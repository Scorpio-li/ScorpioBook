## 1.什么是浮动溢出？
- 在非IE浏览器（如Firefox）下，当容器的高度为auto，且容器的内容中有浮动（float为left或right）的元素，在这种情况下，容器的高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响（甚至破坏）布局的现象。


## 2.清除浮动方法：
- 方法一：使用带clear属性的空元素，在浮动元素后使用一个空元素如：，并在CSS中赋予 .clear{clear:both;}

- 方法二：使用CSS的overflow属性，给浮动元素的容器添加overflow:hidden或overflow:auto.

- 方法三：给浮动的元素的容器添加浮动

- 方法四：使用邻接元素处理,给浮动元素后面的元素添加clear属性。

```js
.content{
  clear:both;
}
```


- 方法五：使用CSS的:after伪元素,结合 :after 伪元素（注意这不是伪类，而是伪元素，代表一个元素之后最近的元素）和 IEhack ，可以完美兼容当前主流的各大浏览器，这里的 IEhack 指的是触发 hasLayout。
给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动。

```js
.clearfix:after{
  content: "020";
  display: block;
  height: 0;
  clear: both;
  visibility: hidden;  
  }
.clearfix {
  /* 触发 hasLayout */
  zoom: 1;
  }
```