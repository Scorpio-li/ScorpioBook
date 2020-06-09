# String(文字)

## 省略

## 1. 多行文字超出省略

### 方法一：使用-webkit-line-clamp

> 如果你只针对webkit内核浏览器或者移动端（移动端浏览器多数是webkit内核），那么使用该方案是最好的了。

```css
.line-camp( @clamp:2 ) {
    text-overflow: -o-ellipsis-lastline;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: @clamp;
    -webkit-box-orient: vertical; 
}

/* -webkit-box-orient: vertical 
在使用 webpack 打包的时候这段代码会被删除掉，
原因是 optimize-css-assets-webpack-plugin 这个插件的问题。 */

/* 可以使用如下写法： */

.line-camp( @clamp:2 ) {
    text-overflow: -o-ellipsis-lastline;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: @clamp;
    /*! autoprefixer: off */
    -webkit-box-orient: vertical;
    /* autoprefixer: on */
}
```

### 方法二：利用绝对定位

首先我们对于一个装内容的容器右边预留一个空间用来放省略号，用 padding-right: 1em; 来预留空间，为啥是1em呢，一个省略号差不多就是1em啦，用em单位是为了响应字体大小。

用绝对定位把省略号定位在这个预留的空间右下角。

```html
<div class="wrap">内容</div>
```

```css
.wrap3 {
    position: relative;
    padding-right: 1em;
    /*max-height是line-height的几倍，想最多显示多少行就几倍*/
    max-height: 3.6em;
    line-height: 1.2em;
    text-align: justify;
    overflow: hidden;
}

.wrap3:before {
    position: absolute;
    right: 0;
    bottom: 0;
    content: '...';
}
```

这样的话，省略号永远都会存在的。所以要解决这个问题，我们用一个跟背景颜色一样的方块遮住省略号，那么关键点就是，怎么知道何时要遮住，何时不遮住呢？

思路： 用于挡住省略号的方块也是绝对定位，靠右定为， right: 0 ，但是 bottom 值就不要设置了，如果不设置的话，该方块会跟着文本内容的实际高度移动，而不是 max-height 的高度。这样的话，当不需要省略时（即不超过 max-height ）时，就刚好是 bottom: 0 的情况，就会挡住省略号。当要进行省略时（即超过 max-height ）就会挡不住省略号了，它自己也会被 overflow: hidden 给隐藏掉了。

```css
.wrap {
    position: relative;
    /*line-height和height要相互配合，显示多少行就省略，就是line-height多少倍数*/
    line-height: 1.2em;
    max-height: 3.6em;
    /*此属性看需求来判断是否设置，因为设置了padding-right，多腾出了点位置，该值一般为padding-right的值的负值*/
    /*margin-left: -1em;*/
    /*此值写死成1em就好，因为省略号大概就是占用1em的空间*/
    padding-right: 1em;
    text-align: justify;
    overflow: hidden;
}

.wrap:before {
    position: absolute;
    right: 0;
    bottom: 0;
    content: '...';
}

.wrap:after {
    position: absolute;
    right: 0;
    /*宽高写死1em就好，因为省略号大概就是占用1em的空间，用来遮挡住省略号，也基本上跟wrap的padding-right一致*/
    width: 1em;
    /*与wrap的行高实际值保持一致*/
    height: 1.2em;
    content: '';
    /*要跟所在背景颜色一致才能遮挡住省略号后觉得没异样*/
    background-color: #fff;
}
```

### 方法三：利用float

```css
.wrap {
    /*需要定高*/
    height: 100px;
    /*用来设置显示多少行才省略，值一般为wrap的height值/行数求得，但是这个行数会受到字体大小的限制*/
    /*字体太大了，设置显示很多行也会很丑，都挤一块了，所以这个实际值，要看具体需求和实践*/
    line-height: 25px;
    /*加上此属性显示效果更佳，就算部分浏览器不支持也影响不大*/
    text-align: justify;
    overflow: hidden;
}

.wrap:before {
    float: left;
    /*这个值可以随意设定，不论单位还是什么*/
    width: 1em;
    height: 100%;
    content: '';
}

.wrap:after {
    float: right;
    /*大小随意，设置em单位最好，可随字体大小变化而自适应*/
    /*如果要采用以下渐变效果，那么这个值要大于before里的width值效果会比较好点*/
	/*值越大，渐变的效果越明显影响的范围越大。*/
    width: 2.5em;
    /*与父元素wrap的行高实际px值一样*/
    height: 25px;
    /*此值要跟自身宽度一样，取负值*/
    margin-left: -2.5em;
    /*此值要跟before宽度一样*/
    padding-right: 1em;
    content: '...';
    text-align: right;
    /*这里开始利用在float布局的基础上进行定位移动了*/
    position: relative;
    /*与父元素wrap的行高实际值一样，取负值*/
    top: -25px;
    left: 100%;
    /*设置渐变效果是为了省略号和内容衔接得自然点，没那么突兀，要注意要跟文字所在的背景的颜色搭配（把white替换成背景色）*/
    background: #fff;
    background: -webkit-gradient(linear, left top, right top, from(rgba(255, 255, 255, 0)), to(white), color-stop(50%, white));
    background: -moz-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
    background: -o-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
    background: -ms-linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
    background: linear-gradient(to right, rgba(255, 255, 255, 0), white 50%, white);
}

.wrap .text {
    float: right;
    /*该值要等于wrap:before的width值*/
    margin-left: -1em;
    width: 100%;
}
```
