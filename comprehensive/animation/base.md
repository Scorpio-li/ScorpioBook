# 前端动画基础

## 1. 基本概念

- 帧：在动画过程中，每一幅静止画面即为一“帧”；

- 帧率：即每秒钟播放的静止画面的数量，单位是fps(Frame per second)或赫兹(Hz)；

- 帧时长：即每一幅静止画面的停留时间，单位一般是ms(毫秒)；

- 丢帧：在帧率固定的动画中，某一帧的时长远高于平均帧时长，导致其后续数帧被挤压而丢失的现象；

- 我们在显示器上看到的动画，每一帧变化都是系统绘制出来的（GPU或者CPU）。它的最高绘制频率受限于显示器的刷新频率（而非显卡，大多数是60Hz或者75Hz）。

- 帧频越高，屏幕上图片闪烁感就越小，稳定性也就越高。人的眼睛不容易察觉75Hz以上刷新频率带来的闪烁感。

## 2.动画的实现方式

### 1. **JavaScript：通过定时器（setTimeout 和 setIterval）来间隔来改变元素样式，或者使用requestAnimationFrame；**
    
#### **requestAnimationFrame**
    
- requestAnimationFrame是浏览器用于定时循环操作的一个接口，类似于setTimeout，主要用途是按帧对网页进行重绘。

- 设置这个API的目的是为了让各种网页动画效果（DOM动画、Canvas动画、SVG动画、WebGL动画）能够有一个统一的刷新机制，从而节省系统资源，提高系统性能，改善视觉效果。代码中使用这个API，就是告诉浏览器希望执行一个动画，让浏览器在下一个动画帧安排一次网页重绘。

- requestAnimationFrame使用一个回调函数作为参数，这个回调函数会在浏览器重绘之前调用，由于功效只是一次性的，所以想实现连续的动效，需要递归调用，示例如下：

```html
<div id="demo" style="position:absolute; width:100px; height:100px; background:#ccc; left:0; top:0;"></div>

<script>
var demo = document.getElementById('demo');
function render(){
    demo.style.left = parseInt(demo.style.left) + 1 + 'px'; //每一帧向右移动1px
}
requestAnimationFrame(function(){
    render();
    //当超过300px后才停止
    if(parseInt(demo.style.left) <= 300) requestAnimationFrame(arguments.callee);
});
</script>
```
- cancelAnimationFrame方法用于取消重绘：

```js
var requestID = requestAnimationFrame(repeatOften);
cancelAnimationFrame(requestID);
```

- 使用requestAnimationFrameAPI的优势如下：

    1. 会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随显示器的刷新频率（60 Hz或者75 Hz）；
    
    2. 在隐藏或不可见的元素中，将不会进行重绘或回流，这当然就意味着更少的的cpu，gpu和内存使用量；
    
- 检查浏览器是否支持这个API
```js
window.requestAnimFrame = (function(){
    return  window.requestAnimationFrame || 
            window.webkitRequestAnimationFrame || 
            window.mozRequestAnimationFrame || 
            window.oRequestAnimationFrame || 
            window.msRequestAnimationFrame || 
            function(/* function FrameRequestCallback */ callback, /* DOMElement Element */ element){
            window.setTimeout(callback, 1000 / 60);
            };
})();
```
        
### 2. **CSS3：transition 和 animation；**

#### Transition

- CSS 中的 transition 属性允许块级元素中的属性在指定的时间内平滑的改变，简单看下其语法规则：

- transition: property duration timing-function delay;

- 具体属性值介绍如下：

值 | 描述
---|---
transition-property | 规定设置过渡效果的 CSS 属性的名称。（none / all / property）
transition-duration | 规定完成过渡效果需要多少秒或毫秒。
transition-timing-function | 规定速度效果的速度曲线。（linear、ease、ease-in、ease-out、ease-in-out、cubic-bezier(n,n,n,n)）
transition-delay | 定义过渡效果何时开始。

#### Animation

- 类似的CSS还提供了一个Animation属性，不过区别于Transition，Animation作用于元素本身而不是样式属性，可以使用关键帧的概念，应该说可以实现更自由的动画效果。

- animation: name duration timing-function delay iteration-count direction;
值 	| 描述
--- | ---
animation-name | 规定需要绑定到选择器的 keyframe 名称。（keyframename、none）
animation-duration |	规定完成动画所花费的时间，以秒或毫秒计。
animation-timing-function 	规定动画的速度曲线。|（linear、ease、ease-in、ease-out、ease-in-out、cubic-bezier(n,n,n,n)）
animation-delay |	规定在动画开始之前的延迟。
animation-iteration-count |	规定动画应该播放的次数。
animation-direction |	规定是否应该轮流反向播放动画。 （normal、alternate）
        
### 3. **HTML5：使用HTML5提供的绘图方式（canvas、svg、webgl）**；

#### Canvas

- canvas是HTML5新增的元素，作为页面图形绘制的容器，可用于通过使用JavaScript中的脚本来绘制图形。例如，它可以用于绘制图形，制作照片，创建动画，甚至可以进行实时视频处理或渲染，Canvas具有如下特点：
    
    - 依赖分辨率，基于位图；
    
    - 不支持事件处理器；
    
    - 弱的文本渲染能力；
    
    - 能够以 .png 或 .jpg 格式保存结果图像；
    
    - 最适合图像密集型的游戏，其中的许多对象会被频繁重绘；

- 大多数 Canvas 绘图 API 都没有定义在 canvas 元素本身上，而是定义在通过画布的getContext()方法获得的一个“绘图环境”对象上。Canvas API也使用了路径的表示法。但是，路径由一系列的方法调用来定义，而不是描述为字母和数字的字符串，比如调用 beginPath() 和 arc() 方法。一旦定义了路径，其他的方法，如 fill()，都是对此路径操作。


#### SVG

- SVG是英文Scalable Vector Graphics的缩写，意为可缩放矢量图形，用来定义用于网络的基于矢量的图形，其使用 XML 格式定义图像，并且具有如下特点：

    - 不依赖分辨率，基于矢量图；
    
    - 支持事件处理器；
    
    - 最适合带有大型渲染区域的应用程序（比如谷歌地图）；
    
    - 复杂度高会减慢渲染速度（任何过度使用 DOM 的应用都不快）；
    
    - 不适合游戏应用；
    
- 来看一个简单的示例，用SVG画了一个圆：
```html
<svg xmlns="http://www.w3.org/2000/svg" version="1.1">
    <rect x="50" y="20" rx="20" ry="20" width="150" height="150"
    style="fill:red;stroke:black;stroke-width:5;opacity:0.5"/>
</svg>
```
- SVG 代码以 svg 元素开始，包括开启标签 svg 和关闭标签 /svg 。这是根元素。width 和 height 属性可设置此 SVG 文档的宽度和高度。version 属性可定义所使用的 SVG 版本，xmlns 属性可定义 SVG 命名空间。

- SVG 的 circle 用来创建一个圆。cx 和 cy 属性定义圆中心的 x 和 y 坐标。如果忽略这两个属性，那么圆点会被设置为 (0, 0)。r属性定义圆的半径。
    
- 下面主要是介绍SVG中的几个用于动画的元素，它们分别是：
    
    - animate：通常放置到一个SVG图像元素里面，用来定义这个图像元素的某个属性的动画变化过程；
    
    - animateMotion：元素也是放置一个图像元素里面，它可以引用一个事先定义好的动画路径，让图像元素按路径定义的方式运动；
    
    - animateTransform：元素对图形的运动和变换有更多的控制，它可以指定图形的变换、缩放、旋转和扭曲等；
    
    - mpath：元素的用法在上面的例子里出现过，它是一个辅助元素，通过它，animateMotion等元素可以引用一个外部的定义的path。让图像元素按这个path轨迹运动；

#### WebGL

- WebGL使得网页在支持HTML canvas标签的浏览器中，不需要安装任何插件，便可以使用基于 OpenGL ES 2.0 的 API 在 canvas 中进行3D渲染。 WebGL 程序由JavaScript的控制代码，和在计算机的图形处理单元（GPU）中执行的特效代码(shader code，渲染代码) 组成。

- WebGL 本质上是基于光栅化的 API，而不是基于 3D 的 API。WebGL 只关注两个方面，即投影矩阵的坐标和投影矩阵的颜色。使用 WebGL 程序的任务就是实现具有投影矩阵坐标和颜色的 WebGL 对象即可。可以使用“着色器”来完成上述任务。顶点着色器可以提供投影矩阵的坐标，片段着色器可以提供投影矩阵的颜色。