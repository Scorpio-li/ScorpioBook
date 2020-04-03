# REM适配

## 1.viewport缩放方法
- 所有宽高像素与视觉稿输出相同，然后通过页面宽度与视觉稿的宽度比率，动态设置 viewport。
- 由于 PC 上没有 viewport 的缩放概念，只能以固定值来设定，所以该方法无法在PC上使用

```js
(function () {
    var docEl = document.documentElement;
    var isMobile = window.isMobile /Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini|Mobi/i.test(navigator.userAgent);

    function setScale() {
        var pageScale = 1;

        if (window.top !== window) {
            return pageScale;
        }

        var width = docEl.clientWidth || 360;
        var height = docEl.clientHeight || 640;
        if (width / height >= 360 / 640) {
            // 高度优先
            pageScale = height / 640;
        } else {
            pageScale = width / 360;
        }

        var content = 'width=' + 360 + ', initial-scale=' + pageScale 
          + ', maximum-scale=' + pageScale + ', user-scalable=no';
        document.getElementById('viewport').setAttribute('content', content);

        window.pageScale = pageScale;
    }

    if (isMobile) {
        setScale();
    } else {
        docEl.className += ' pc';
    }
})()
```
<!-- more -->
## 2. rem 布局适配方案
- 按照设计稿与设备宽度的比例，动态计算并设置 html 根标签的 font-size 大小；
- css 中，设计稿元素的宽、高、相对位置等取值，按照同等比例换算为 rem 为单位的值；
- 设计稿中的字体使用 px 为单位，通过媒体查询稍作调整。

### 2.1 动态设置 html 标签 font-size 大小
    
```js
(function(WIN) {
    var  setFontSize = WIN.setFontSize = function (_width) {
        var  docEl = document.documentElement; 
        // 获取当前窗口的宽度
        var  width = _width || docEl.clientWidth; // docEl.getBoundingClientRect().width;

        // 大于 1080px 按 1080
        if (width > 1080) { 
            width = 1080;
        }

        var  rem = width / 10;
        console.log(rem);

        docEl.style.fontSize = rem + 'px';

        // 部分机型上的误差、兼容性处理
        var  actualSize = win.getComputedStyle && parseFloat(win.getComputedStyle(docEl)["font-size"]);
        if (actualSize !== rem && actualSize > 0 && Math.abs(actualSize - rem) > 1) {
            var remScaled = rem * rem / actualSize;
            docEl.style.fontSize = remScaled + 'px';
        }
    }

    var timer;
    //函数节流
    function dbcRefresh() {
        clearTimeout(timer);
        timer = setTimeout(setFontSize, 100);
    }

    //窗口更新动态改变 font-size
    WIN.addEventListener('resize', dbcRefresh, false);
    //页面显示时计算一次
    WIN.addEventListener('pageshow', function(e) {
        if (e.persisted) { 
            dbcRefresh() 
        }
    }, false);
    setFontSize();
})(window)
```
- 对于全屏显示的 H5 活动页，对宽高比例有所要求，此时应当做的调整。

```js
function adjustWarp(warpId = '#warp') {
    // if (window.isMobile) return;
    const $win = $(window);
    const height = $win.height();
    let width = $win.width();

    // 考虑导航栏情况
    if (width / height < 360 / 600) {
        return;
    }

    width = Math.ceil(height * 360 / 640);

    $(warpId).css({
        height,
        width,
        postion: 'relative',
        top: 0,
        left: 'auto',
        margin: '0 auto'
    });

    // 重新计算 rem
    window.setFontSize(width);
}
```
        
### 2.2 元素大小取值方法

1. 以设计稿宽度 1080px 为例，我们将宽度分为 10 等份以便于换算，那么 1rem = 1080 / 10 = 108px。
```js
const px2rem = function(px, rem = 108) {
    let remVal = parseFloat(px) / rem;

    if (typeof px === "string" && px.match(/px$/)) { 
        remVal += 'rem';
    }

    return remVal;
}
```

### 2.3 rem 布局方案的开发方式
```cs
// px 转 rem
.px2rem(@px, @attr: 'width', @rem: 108rem) {
    @{attr}: (@px / @rem);
}

.px2remTLWH(@top, @left, @width, @height, @rem: 108rem) {
    .px2rem(@top, top, @rem);
    .px2rem(@left, left, @rem);
    .px2rem(@width, width, @rem);
    .px2rem(@height, height, @rem);
}
```
### 2.4 字体使用 px 为单位

- 由于字体的缩放比例显然与长度单位是不同步的，所以字体不适合使用 rem 作为单位。

文字依然使用 px 为单位，然后针对性使用媒体查询设置几种大小即可。

```html
// 字体响应式
@media screen and (max-width: 321px) {
    body {
        font-size: 12px;
    }
}

@media screen and (min-width: 321px) and (max-width: 400px) {
    body {
        font-size: 14px;
    }
}

@media screen and (min-width: 400px) {
    body {
        font-size: 16px;
    }
}

```