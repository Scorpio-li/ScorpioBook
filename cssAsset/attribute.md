# CSS3属性与变量

## 1. border-radius
- 语法：border-radius: [左上] [右上] [右下] [左下]
- 语法：border-radius:x半径/y半径


## 2. ::after
- eg:放大镜

```css
div {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    border: 5px solid #333;
    position: relative;
}
div::after {
    content: '';
    display: block;    
    width: 8px;    
    height: 60px;    
    border-radius: 5px;    
    background: #333;    
    position: absolute;    
    right: -22px;    
    top: 38px;    
    transform: rotate(-45deg);
}
```

## 3. attr和content:
- css3提供的attr：能够在css中获取到元素的某个属性值，然后插入到伪元素的content中去。
- html代码：

```html
<div data-title=“Hello World!”>hello</div>
```

- 我们来看看实现这个插件的css代码：
```css
div {
    position: relative;
}
div:hover::after {
    content: attr(data-title);    //取到data-title属性的值
    display: inline-block;
    padding: 10px 14px;
    border: 1px solid #ddd;
    border-radius: 5px;
    position: absolute;
    top: -50px;
    left: -30px;
}
```
- 当hover的时候，在元素尾部添加一个内容为data-title属性值的元素，所以就实现了hover显示的效果，如下图所示：

## 4.box-sizing
- 在标准盒子模型中，元素的总宽＝content + padding + border + margin。
box-sizing属性就是用来重定义这个计算方式的，它有三个取值，分别是：content-box（默认）、border-box、padding-box
一般来说，假如我们需要有一个占宽200px、padding10px、border5px的div，经过计算，要这么定义样式。

```css
div {
    width: 170px;   //这里的宽度要使用200-10*2-5*2 = 170得到。
    height: 50px;
    padding: 10px;
    border: 5px solid red;
}
```
- 然后我们来使用一下box-sizing属性。
```css
div {
    box-sizing: border-box;
    width: 200px;  //这里的宽度就是元素所占总宽度，不需要计算  
    height: 50px;
    padding: 10px;
    border: 5px solid red;
}
```

## 5. 使用:not()去除导航上不需要的边框

```css
/* 添加边框 */
.nav li {
    border-right:1px solid #666;
}
/* 然后去除最后一个元素的边框 */
.nav li:last-child {
    border-right:none;
}
/* 或 */
.nav li:not(:last-child){
    border-right:1px solid #666;
}

```

## 6. css变量--> :root{}
- 设置页面基本css样式数值：

```css
:root {
   --base-font-size:30px; 
   --columns:200px 200px;
   --base-margin:30px;
}

/* 设置页面样式 */
#nav {
    margin : var(--base-margin) 0;
    font-size: var(--base-font-size);
}

/* 媒体查询中修改这些变量值:即可修改页面样式 */
@media all and (max-width: 450px){
    :root {
       --base-font-size:20px; 
       --columns:200px 100px;
       --base-margin:20px;
    }
}
```

## 7. css选择器

### 1. *
- 星号呢会将页面上所有每一个元素都选到。许多开发者都用它来清空margin和padding。
- 也可以用来选择某元素的所有子元素。

```css
#container * {
  border: 1px solid black;
}
```
### 2. #X：#可以用id来定位某个元素
### 3. .X:class选择器
### 4. X Y：后代选择器
### 5. X:标签选择器
### 6. X:visited ， Y:link ， Z:hover
- link这个伪类来定位所有还没有被访问过的链接。
- visited来定位所有已经被访问过的链接。
- hover通常大家在鼠标飘过锚点链接时候加下边框的时候用到它。

### 7. X+Y:
相邻选择器，它指挥选中指定元素的直接后继元素。

### 8. X>Y:
子选择器，X Y和X > Y的差别就是后面这个指挥选择它的直接子元素。

### 9. X~Y:
X Y和X > Y的差别就是后面这个指挥选择它的直接子元素。

### 10. X[title]:
属性选择器，自会选择有title属性的元素。
### 11. X[href="foo"]：
只会选择属性为具体值的元素。
### 12. X[href*="strongme"]：
- 指定了strongme这个值必须出现在锚点标签的href属性中，不管是strongme.cn还是strongme.com还是www.strongme.cn都可以被选中。
- 但是记得这是个很宽泛的表达方式。如果锚点标签指向的不是strongme相关的站点，如果要更加具体的限制的话，那就使用^和$，分别表示字符串的开始和结束。

### 13. X[href^="http"]：
定位锚点属性href中以http开头的标签

### 14. X[href$=".jpg"]:
去搜索所有的图片链接，或者其它链接是以.jpg结尾的。但是记住这种写法是不会对gifs和pngs起作用的。

### 15. X[data-*="foo"]:
给标签加自定义属性data-* ，eg:a[data-filetype="image"]

### 16. X[foo~="bar"]:
这个~符号可以定位那些某属性值是空格分隔多值的标签。

```html
<a href="path/to/image.jpg" data-info="external image"> Click Me, Fool </a>

/* Target data-info attr that contains the value "external" */
a[data-info~="external"] {
   color: red;
}

/* And which contain the value "image" */
a[data-info~="image"] {
  border: 1px solid black;
}
```

### 17. X:checked:定位选中的单选框或多选框

### 18. X:after:
before和after这俩伪类。它们会在被选中的标签周围生成一些内容。

```css
/* 这段代码会在目标标签后面补上一段空白，然后将它清除 */
.clearfix:after {
    content: "";
    display: block;
    clear: both;
    visibility: hidden;
    font-size: 0;
    height: 0;
  }

.clearfix { 
   *display: inline-block; 
   _height: 1%;
}
```
### 19. X:not(selector)
取反伪类,或者说我想选中所有出段落标签之外的所有标签。

### 20. X::pseudoElement
- 我们可以使用::来选中某标签的部分内容，如地一段，或者是第一个字没有。但是记得必须使用在块式标签上才起作用。
- eg:定位第一个字p::first-letter。会找到页面上所有段落，并且指定为每一段的第一个字。 
- eg:定位某一段的第一行p::first-line

### 21. X:nth-child(n)
nth-child接受一个整形参数，然后它不是从0开始的。如果你想获取第二个元素那么你传的值就是li:nth-child(2).

### 22. X:nth-last-child
它是从结尾处开始的，倒回去的。

### 23. X:nth-of-type(n)
- 曾几何时，我们不想去选择子节点，而是想根据元素的类型来进行选择。
- 想象一下有5个ul标签。如果你只想对其中的第三个进行修饰，而且你也不想使用id属性，那你就可以使用nth-of-type(n)伪类来实现了：ul：nth-of-type(3)


### 24. nth-last-of-type(n)

### 25. X:first-child

### 26. X:last-child

### 27. X:only-child
它允许你获取到那些只有一个子标签的父标签。

### 28. X:only-of-type
它会定位某标签只有一个子标签的目标。

### 29. X:first-of-type
first-of-type伪类可以选择指定标签的第一个兄弟标签。