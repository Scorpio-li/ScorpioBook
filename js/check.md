## 1. 碰撞检测

```js
// 碰撞检测
/*
*2D空间碰撞检测
1. 矩形碰撞矩形:
rectB.x > rectA.x - rectB.width &&
rectB.x < rectA.x + rectA.width + rectB.width &&
rectB.y > rectA.y - rectB.height &&
rectB.y < rectA.y + rectA.height + rectB.height

2.圆形碰撞圆形:只要两圆的圆小于两圆的半径之和就能认定两圆发生了碰撞
Math.sqrt(Math.pow(circleA.x - circleB.x, 2) + Math.pow(circleA.y - circleB.y, 2)) < circleA.radius + circleB.radius

3.圆形和矩形的碰撞:将圆形看成一个矩形，用矩形与矩形之间的那套方法来检测碰撞。
circle.x > rect.x - circle.radius &&
circle.x < rect.x + rect.width + circle.radius &&
circle.y > rect.y - circle.radius &&
circle.y > rect.y + rect.height + circle.radius

*/


// 分离轴检测
(function(global, doc) {
    var inherit, extend, Vector, Projection,
        Shape, Polygon, Point, Circle, Line,
        getPolygonPointClosestToCircle, polygonCollidesWithCircle,
        polygonCollidesWithPolygon, circleCollidesWithCircle,
        shapeCollideswithLine;

    // 对象扩展................................
    extend = function extend(target, obj) {
        var prop, val;
        if (!Array.isArray(obj)) {
            for (prop in obj) {
                val = obj[prop];
                if (typeof val === 'object') {
                    target[prop] = Array.isArray(val) ? [] : {};
                    extend(target[prop], val);
                } else {
                    target[prop] = val;
                }
            }
        } else {
            for (prop = 0; prop < obj.length; prop++) {
                val = obj[prop];
                if (typeof val === 'object') {
                    target[prop] = Array.isArray(val) ? [] : {};
                    extend(target[prop], val);
                } else {
                    target[prop] = val;
                }
            }
        }
    };

    // 原型继承.................................
    inherit = function(Child, Parent) {
        var Temp = function() {
            this.constructor = Child;
        };
        Temp.prototype = Parent.prototype;
        Child.prototype = new Temp();
    };

    // 获取多边形上最靠近圆形的点...................
    getPolygonPointClosestToCircle = function(polygon, circle) {
        var min = Infinity,
            closestPoint, length;

        polygon.points.forEach(function(point) {
            length = Math.pow(circle.x - point.x, 2) + Math.pow(circle.y - point.y, 2);
            if (length < min) {
                min = length;
                closestPoint = point;
            }
        });

        return closestPoint;
    };

    // 圆形碰撞圆形...........................................
    circleCollidesWithCircle = function(c1, c2) {
        var distace = Math.sqrt(Math.pow(c1.x - c2.x, 2) + 
                                Math.pow(c1.y - c2.y, 2));
        return {
            axis: (new Vector(c1.x - c2.x, c1.y - c2.y)).normalize(),
            overlap: c1.radius + c2.radius - distace
        }
    };

    // 多边形碰撞多边形.........................................
    polygonCollidesWithPolygon = function(p1, p2) {
        var axes = p1.getAxes();
        axes = axes.concat(p2.getAxes());
        return p1.minimumTranslationVector(axes, p2);
    };

    // 多边形和圆形之间的碰撞................................
    polygonCollidesWithCircle = function(polygon, circle) {
        var axes = polygon.getAxes(),
            closestPoint = getPolygonPointClosestToCircle(polygon, circle),
            v1, v2;

        v1 = new Vector(closestPoint.x, closestPoint.y);
        v2 = new Vector(circle.x, circle.y);

        axes.push(v1.edge(v2).normalize());

        return polygon.minimumTranslationVector(axes, circle);
    };

    // 图形和直线之间的碰撞...................................
    shapeCollideswithLine = function(shape, line) {
        var axes = line.getAxes();
        return shape.minimumTranslationVector(axes, line);
    };

    // 矢量.....................................
    Vector = function(point) {
        if (arguments.length === 1) {
            this.x = point.x;
            this.y = point.y;
        } else {
            this.x = arguments[0];
            this.y = arguments[1];
        }
    };

    extend(Vector.prototype, {
        getMagnitude: function() {
            return Math.sqrt(Math.pow(this.x, 2) + Math.pow(this.y, 2));
        },
        add: function(vector) {
            return new Vector(this.x + vector.x, this.y + vector.y);
        },
        subtract: function(vector) {
            return new Vector(this.x - vector.x, this.y - vector.y);
        },
        dotProduct: function(vector) {
            return this.x * vector.x + this.y * vector.y;
        },
        edge: function(vector) {
            return this.subtract(vector);
        },
        prependicular: function() {
            return new Vector(this.y, -this.x);
        },

        // 获取单位向量
        normalize: function() {
            var v = new Vector(0, 0),
                m = this.getMagnitude();
            if (m !== 0) {
                v.x = this.x / m;
                v.y = this.y / m;
            }
            return v;
        },

        // 获取法向量
        normal: function() {
            return this.prependicular().normalize();
        }
    });

    // 投影.....................................
    Projection = function(min, max) {
        this.min = min;
        this.max = max;
    };

    Projection.prototype.overlap = function(projection) {
        return Math.min(this.max, projection.max) - Math.max(this.min, projection.min);
    };

    // 形状.....................................
    Shape = function() {};

    extend(Shape.prototype, {
        collidesWith: function(anotherShape) {
            var axes = this.getAxes().concat(anotherShape.getAxes()),
                mtv;

            return mtv.overlap > 0 ? true : false;
        },

        // 检查每个轴上投影的间隔，存在返回最小偏移量
        minimumTranslationVector: function(axes, anotherShape) {
            var minOverlap = Infinity,
                i, axis, projection1, projection2, 
                overlap, axisWithSmallOverlap;

            for (i = 0; i < axes.length; i++) {
                axis = axes[i];
                projection1 = this.project(axis);
                projection2 = anotherShape.project(axis);
                overlap = projection1.overlap(projection2);
                if (overlap < minOverlap) {
                    axisWithSmallOverlap = axis;
                    minOverlap = overlap;
                }
                if (overlap <= 0) break;
            }

            return {
                axis: axisWithSmallOverlap,
                overlap: minOverlap
            };
        },

        isPointInPath: function(context, x, y) {
            this.createPath(context);
            return context.isPointInPath(x, y);
        },

        run: function(dTime) {
            this.velocity.x = this.lastVelocity.x;
            this.velocity.y = this.lastVelocity.y;
            this.move(this.velocity.x * dTime / 1000, this.velocity.y * dTime  / 1000);
        },

        // 获取轴线
        getAxes: function() {
            throw 'getAxes() not implemented';
        },

        // 获取在某一轴线上的投影
        project: function(axis) {
            throw 'project(axis) not implemented';
        },

        move: function() {
            throw 'move(x, y) not implemented';
        }
    });

    // 点..........................................
    Point = function(point) {
        if (arguments.length === 1) {
            this.x = point.x;
            this.y = point.y;
        } else {
            this.x = arguments[0];
            this.y = arguments[1];
        }
    };

    // 多边形......................................
    Polygon = function(points, velocity) {
        this.points = points || [];
        this.lastVelocity = velocity || {
            x: 10,
            y: 10
        };
        this.velocity = {};
        this.velocity.x = this.lastVelocity.x;
        this.velocity.y = this.lastVelocity.y;
    };

    inherit(Polygon, Shape);

    extend(Polygon.prototype, {
        collidesWith: function(anotherShape) {
            if (anotherShape instanceof Circle) {
                return polygonCollidesWithCircle(this, anotherShape);
            } else if (anotherShape instanceof Polygon) {
                return polygonCollidesWithPolygon(this, anotherShape);
            } else if (anotherShape instanceof Line) {
                return shapeCollideswithLine(this, anotherShape);
            }
        },
        project: function(axis) {
            var scalars = [],
                v = new Vector();
            this.points.forEach(function(point) {
                v.x = point.x;
                v.y = point.y;
                scalars.push(v.dotProduct(axis));
            });
            return new Projection(Math.min.apply(Math, scalars),
                                  Math.max.apply(Math, scalars));
        },
        getAxes: function() {
            var v1 = new Vector(),
                v2 = new Vector(),
                axes = [];

            this.points.forEach(function(point, i, points) {
                v1.x = point.x;
                v1.y = point.y;

                if (i + 1 < points.length) {
                    v2.x = points[i + 1].x;
                    v2.y = points[i + 1].y;
                } else {
                    v2.x = points[0].x;
                    v2.y = points[0].y;
                }

                axes.push(v1.edge(v2).normal());
            });

            return axes;
        },
        centroid: function() {
            var result = {
                x: 0,
                y: 0
            },
            n = this.points.length;
            this.points.forEach(function(point) {
                result.x += point.x;
                result.y += point.y;
            });
            result.x /= n;
            result.y /= n;
            return result;
        },
        addPoint: function(x, y) {
            this.points.push(new Point(x, y));
        },
        move: function(dX, dY) {
            this.points.forEach(function(point) {
                point.x += dX;
                point.y += dY;
            });
        },
        createPath: function(context) {
            context.beginPath();
            this.points.forEach(function(point) {
                context.lineTo(point.x, point.y);
            });
            context.closePath;
        },
        draw: function(context) {
            this.createPath(context);
            context.fill();
        }
    });

    // 圆形.......................................
    Circle = function(x, y, radius, velocity) {
        this.x = x;
        this.y = y;
        this.radius = radius;
        this.lastVelocity = velocity || {
            x: 10,
            y: 10
        };
        this.velocity = {};
        this.velocity.x = this.lastVelocity.x;
        this.velocity.y = this.lastVelocity.y;
    };

    inherit(Circle, Shape);

    extend(Circle.prototype, {
        collidesWith: function(anotherShape) {
            if (anotherShape instanceof Circle) {
                return circleCollidesWithCircle(this, anotherShape);
            } else if (anotherShape instanceof Polygon) {
                return polygonCollidesWithCircle(anotherShape, this);
            } else if (anotherShape instanceof Line) {
                return shapeCollideswithLine(this, anotherShape);
            }
        },
        getAxes: function() { return; },
        project: function(axis) {
            var dotProduct = new Vector(this.x, this.y).dotProduct(axis);
            return new Projection(dotProduct - this.radius, dotProduct + this.radius);
        },
        centroid: function() {
            return {
                x: this.x,
                y: this.y
            }
        },
        createPath: function(context) {
            context.beginPath();
            context.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
            context.closePath();
        },
        draw: function(context) {
            this.createPath(context);
            context.fill();
        },
        move: function(dX, dY) {
            this.x += dX;
            this.y += dY;
        }
    });

    // 直线
    Line = function(point, vector) {
        if (arguments.length === 2) {
            this.x = point.x;
            this.y = point.y;
            this.vector = vector;
        } else {
            this.x = arguments[0];
            this.y = arguments[1];
            this.vector = arguments[2];
        }
    };

    inherit(Line, Shape);

    extend(Line.prototype, {
        getAxes: function() {
            return [this.vector.normal()];
        },
        project: function(axis) {
            var n = axis.dotProduct(this);
            return new Projection(n, n + 1);
        },
        centroid: function() {
            return {
                x: this.x,
                y: this.y
            }
        }
    });

    global.Circle = Circle;
    global.Polygon = Polygon;
    global.Point = Point;
    global.Shape = Shape;
    global.Vector = Vector;
    global.Line = Line;
})(this, this.document);

(function(global, doc) {
    var canvas = document.getElementById('mycanvas'),
        cxt = canvas.getContext('2d'),
        QuadTree = global.QuadTree,
        Rect = global.Rect,
        w = 600,
        h = 300,
        rectArr = [],
        tree, i, len, time;

    // 设置canvas尺寸
    canvas.setAttribute('width', w);
    canvas.setAttribute('height', h);
    
    cxt.fillStyle = '#000';

    var windowToCanvas = function(canvas, x, y) {
        var bounds = canvas.getBoundingClientRect();
        
        return {
            x: (x - bounds.left) * (canvas.width / bounds.width),
            y: (y - bounds.top) * (canvas.height / bounds.height)
        };
    };

    var polygonPoints = [
            [new Point(250, 130), new Point(250, 250),
             new Point(350, 250), new Point(400, 150)],
            [new Point(410, 130), new Point(410, 200),
             new Point(490, 100), new Point(450, 10)]
        ],
        c1 = new Circle(50, 50, 40, {x: 100, y: 100}),
        c2 = new Circle(100, 200, 20),
        p1 = new Polygon(polygonPoints[0], {x: 50, y: 80}),
        p2 = new Polygon(polygonPoints[1], {x: -30, y: -60}),
        lastLoc = {},
        shapes = [],
        shapeBeingDrag;

    shapes.push(p1, p2);

    shapes.forEach(function(shape) {
        shape.draw(cxt);
    });

    canvas.addEventListener('mousedown', function(e) {
        var loc = windowToCanvas(this, e.clientX, e.clientY);
        shapes.every(function(shape) {
            if (shape.isPointInPath(cxt, loc.x, loc.y)) {
                shapeBeingDrag = shape;
                lastLoc.x = loc.x;
                lastLoc.y = loc.y;
                return false;
            }
            return true;
        });
    });

    canvas.addEventListener('mouseup', function(e) {
        shapeBeingDrag = null;
    });

    var separate = function(shape, mtv, velocity) {
        dX = mtv.axis.x * mtv.overlap;
        dY = mtv.axis.y * mtv.overlap;
        if (dX * velocity.x > 0) dX = -dX;
        if (dY * velocity.y > 0) dY = -dY;
        shape.move(dX, dY);
    };

    canvas.addEventListener('mousemove', function(e) {
        var loc, velocity;
        if (shapeBeingDrag) {
            cxt.clearRect(0, 0, w, h);


            loc = windowToCanvas(this, e.clientX, e.clientY);
            velocity = {
                x: loc.x - lastLoc.x,
                y: loc.y - lastLoc.y
            };
            shapeBeingDrag.move(loc.x - lastLoc.x, loc.y - lastLoc.y);
            shapes.forEach(function(shape, i) {
                var isCollided = false,
                    j, mtv;
                for (j = 0; j < shapes.length; j++) {
                    if (j === i) continue;
                    mtv = shape.collidesWith(shapes[j]);
                    isCollided = mtv.overlap > 0 ? true : false;
                    if (isCollided) break;
                }
                if (isCollided) {
                    separate(shapeBeingDrag, mtv, velocity);
                    cxt.save();
                    shape.draw(cxt);
                    cxt.restore();
                } else {
                    shape.draw(cxt);
                }
            });

            lastLoc.x = loc.x;
            lastLoc.y = loc.y;
        }
    });

    var bounce = function(mtv, collider, collidee) {
        var centroid1 = new Vector(collider.centroid()),
            centroid2 = new Vector(collidee.centroid()),
            centroidVector = centroid1.subtract(centroid2),
            dotProductRatio, lastVelocity;

        if (mtv.axis.dotProduct(centroidVector) < 0) {
            mtv.axis.x = -mtv.axis.x;
            mtv.axis.y = -mtv.axis.y;
        }

        if (mtv.axis.dotProduct(collider.velocity) > 0) {
            return;
        }

        dotProductRatio = Math.abs(2 * mtv.axis.dotProduct(collider.velocity) / 
            mtv.axis.dotProduct(mtv.axis));

        mtv.axis.x *= dotProductRatio;
        mtv.axis.y *= dotProductRatio;

        lastVelocity = mtv.axis.add(collider.velocity);

        collider.lastVelocity.x = lastVelocity.x;
        collider.lastVelocity.y = lastVelocity.y;
    };

    var bounds = [
        new Line(0, 0, new Vector(1, 0)),
        new Line(0, 0, new Vector(0, 1)),
        new Line(0, h, new Vector(1, 0)),
        new Line(w, 0, new Vector(0, 1))
    ];

    draw = function() {
        cxt.clearRect(0, 0, w, h);
        shapes.forEach(function(shape, i) {
            var mtv, j;
            shape.run(16);

            for (j = 0; j < shapes.length; j++) {
                if (j === i) continue;
                mtv = shape.collidesWith(shapes[j]);
                if (mtv.overlap > 0) {
                    separate(shape, mtv, shape.velocity);
                    bounce(mtv, shape, shapes[j]);
                }
            }

            for (j = 0; j < bounds.length; j++) {
                mtv = shape.collidesWith(bounds[j]);
                if (mtv.overlap > 0) {
                    separate(shape, mtv, shape.velocity);
                    bounce(mtv, shape, bounds[j]);
                }
            }

            shape.draw(cxt);
        });
        requestAnimationFrame(draw);
    };
    
    var startButton = document.getElementById('start-button');
    startButton.addEventListener('click', function() {
        requestAnimationFrame(draw);
    });
    
})(this, this.document);
```