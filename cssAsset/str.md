# String(文字)

## 1. 文字超出省略
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