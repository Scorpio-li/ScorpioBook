# CSS核心概念

## 1、选择器

### 1.1 选择器类型

- **简单选择器**：通过元素类型 tagName、*、.class 或 #id 匹配一个或多个元素。

- **属性选择器**：通过 属性 / 属性值 匹配一个或多个元素。

类型 | 匹配结果
---|---
[ attr ] | 匹配包含 attr 属性的所有元素
[ attr = val ]	| 匹配 attr 属性值为 val 的所有元素
[ attr ~= val ]	| 匹配 attr 属性中包含 val 词汇( space-separated )的所有元素
[ attr ^= val ]	| 匹配 attr 属性中以 val 开头的所有元素
[ attr &#124;= val ]	| 匹配 attr 属性中以 val或者 val- 开头的所有元素
[ attr $= val ]	| 匹配 attr 属性中以 val 结尾的所有元素
[ attr *= val ]	| 匹配 attr 属性中包含 val 的所有元素

- 伪类和伪元素
    1. 伪类：匹配元素的相关状态和属性，如 :hover :first-child :nth-child() ，单冒号。
    
    2. 伪元素：匹配元素的相关位置, 如 ::after ::first-letter ::selection，双冒号。

- **组合选择器**：

类型 | 组合 | 匹配结果
---|---|---
选择器组 | A , B | 匹配 A or B选择器规则
后代选择器 | A   B | 匹配B选择器规则，且B是A的后代（子孙）
子代选择器 | A > B | 匹配B选择器规则，且B是A的子代（必须是直接子代）
相邻兄弟选择器 | A + B | 匹配B选择器规则，且B是A的弟弟（AB属于同一父代，且B紧跟A的后面）
任一兄弟选择器 | A - B | 匹配B选择器规则，且B是A的任意弟弟（AB属于同一父代，且B在A之后，不一定紧挨）


### 1.2 选择器优先级

- 优先级按以下规则递增：
    - 通配符 * 、组合选择器( , > + - '')和否定伪类:not()对优先级没有影响（在 :not() 内部声明的选择器还是会按照规则影响）
    
    - 浏览器默认样式
    
    - 元素类型选择器 tagName、伪元素选择器 ::
    - 类选择器 .class、 属性选择器 [ attr ]、伪类选择器 :
    - id选择器 #id
    - 内联样式 < tagName style="" >
    - !important
- css权重表

选择器 | 用法 | 权重值
---|---|---
!important | 放在属性值后， 如color: red !important; | 10000
内联样式 | style="xxx" | 1000
ID选择器 | #box | 100
类、伪类、属性选择器 | .box、:hover、div[class=box] | 10
标签选择器和伪元素选择器 | p、:before | 1
通配符* 子选择器> 相邻选择器+ 同胞选择器~ | 略 | 0


### 1.3 具体类型

#### 1. *
- 星号呢会将页面上所有每一个元素都选到。许多开发者都用它来清空margin和padding。
- 也可以用来选择某元素的所有子元素。

```css
#container * {
  border: 1px solid black;
}
```
#### 2. #X（ID选择器）：#可以用id来定位某个元素
#### 3. .X:class（类）选择器
#### 4. X Y：后代选择器
#### 5. X:标签选择器
```html
<p> hello world </p>
<p> 你好呀~ </p>

<!--css-->
p {
    color: red;
}
```


#### 7. X+Y:
相邻选择器，它指挥选中指定元素的直接后继元素。
```html
<div class="main">
  <h1>标题</h1>
  <p>段落</p>
</div>
<!--css-->
h1 + p {
  color: red; // 段落字体变红色
}
```
#### 8. X>Y:
子选择器，X Y和X > Y的差别就是后面这个指挥选择它的直接子元素。

#### 9. X~Y:(同胞选择器)
以selectorA~selectorB形式，表示选择指定元素所有符合条件的所有兄弟元素， 他可能有多个兄弟
```html
<div class="main">
  <h1>标题</h1>
  <p>段落1</p>
  <p>段落2</p>
</div>
<!--css-->
<!--符合两个条件：1：h1的兄弟元素； 2：凡是p标签包裹的-->
h1 ~ p {
  color: red;  // 段落1、2字体都变红
}
```

#### 10. XY(交集选择器)

- 以selectorA.selectorB形式，表示既符合选择器A又符合选择器B的元素
```html
<ul>
  <li class="item"> btn1 </li>
  <li class="item active"> btn2 </li>
</ul>
<!--css-->
.item.active {
  color: red;  // 表示有active类的，又有item类的。
}
```

#### 10. X,Y(并集选择器)
- 以seltorA,selectorB逗号分隔的形式，表示不同的选择器A和选择器B的元素都应用同一种样式。

```html
<div class="box1"> 段落1 </div>
<div class="box2"> 段落2 </div>
<!--css-->
.box1, .box2 {
  color: red;
}
```
#### 10. 属性选择器
##### 10. X[attr]: [attr]表示选择所有带有attr属性的标签

- 属性选择器，自会选择有attr属性的元素。

```html
<p title="hello world"> hello world </p>
<p title="test"> 你好呀~ </p>

<!--css-->
p[title] {
  color: red;
}
```
##### 11. X[href="foo"]：[attr=xxx]表示用来选择有attr属性且属性值等于xxx的元素，注意属性值必须完全相等

- 只会选择属性为具体值的元素。

```html
<input class="input text" type="text" value="hello world"/>

<!--css-->
input[type=text] {
  color: red;
}
// or
input[class="input text"]{
  color: red;
}
```

##### 12. X[href*="strongme"]：
- 指定了strongme这个值必须出现在锚点标签的href属性中，不管是strongme.cn还是strongme.com还是www.strongme.cn都可以被选中。
- 但是记得这是个很宽泛的表达方式。如果锚点标签指向的不是strongme相关的站点，如果要更加具体的限制的话，那就使用^和$，分别表示字符串的开始和结束。

##### 13. X[href^="http"]：
定位锚点属性href中以http开头的标签
```html
<div class="box"> box <div>
<div class="box-sm"> box <div>
<div class="box_lg"> box <div>
<!--css-->
div[class^=box] {
  color: red;
}
```

##### 14. X[href$=".jpg"]:
去搜索所有的图片链接，或者其它链接是以.jpg结尾的。但是记住这种写法是不会对gifs和pngs起作用的。
```html
<div class="box"> box <div>
<div class="box red blue"> box <div>
<div class="box _red"> box <div>
<!--css -->
<!--这里以red结尾的样式类必须写在最后，否则有可能会被后面的样式覆盖-->
div[class$=red] {
  color: red;
}
```
##### 15. X[data-*="foo"]:
给标签加自定义属性data-* ，eg:a[data-filetype="image"]
```html
<div class="box-sm"> box <div>
<div class="box sm blue"> box <div>
<div class="box _sm"> box <div>
<!--css -->
div[class*=sm]{
  color: red;
}
```
##### 16. X[foo~="bar"]: 表示包含某个类的元素，多个类中的其中一个类名必须和xxx相等
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

##### 17. X[attr|=xxx] :表示选择属性值为xxx（这里必须是相等的）或者 以xxx-属性开头的元素
```html
<div class="box"> box <div>
<div class="box-sm"> box <div>

<!--这里的div不会生效, 这里必须是 box- 开头-->
<div class="box_lg"> box <div>
<!--css-->
div[class|=box] {
  color: red;
}
```
#### 11. 伪类选择器

以selector加:的的形式，CSS 伪类用于向某些选择器添加特殊的效果，这里只列举常见的几种：

- 表示状态

选择器 | 作用 | 栗子
---|---|---
x:link | 未访问的链接 | a:link
x:visited | 已访问的链接 | a:visited
x:hover | 鼠标移动到链接上 | a:hover
x:active | 选定的链接 | a:acitve
x:focus | 选定元素聚焦时的样式 | input:focus

- 表示结构:

选择器 | 作用 | 栗子
---|---|---
x:first-child | 第一个子元素为x | ul li:first-child
x:last-child | 最后一个子元素为x | ul li:last-child
x:nth-child(n) | 第n个位置的子元素x，不分元素类型 | ul li:nth-child(even)
x:nth-last-child(n) | 同上，倒数第n个位置的子元素x | ul li:nth-last-child(2)
x:only-child | 唯一子元素为x | a span:only-child
x:only-of-type | 唯一子元素为x, 且x没有其他同类型的兄弟元素 | a span:only-of-type

- 表单相关:

选择器 | 作用 | 栗子
---|---|---
x:empty | 空标签（有空格也不行） | span:empty
x:checked | 勾选input的状态（值为true或false） | input:checked
x:disabled | 表单元素是否禁用（值为true或false） | input:disabled
x:required | 表单元素是必填项时设置指定样式 | input:required

##### 6. X:visited ， Y:link ， Z:hover
- link这个伪类来定位所有还没有被访问过的链接。
- visited来定位所有已经被访问过的链接。
- hover通常大家在鼠标飘过锚点链接时候加下边框的时候用到它。
##### 17. X:checked:定位选中的单选框或多选框
##### 18. X:after:
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
##### 19. X:not(selector)
取反伪类,或者说我想选中所有出段落标签之外的所有标签。

##### 20. X::pseudoElement
- 我们可以使用::来选中某标签的部分内容，如地一段，或者是第一个字没有。但是记得必须使用在块式标签上才起作用。
- eg:定位第一个字p::first-letter。会找到页面上所有段落，并且指定为每一段的第一个字。 
- eg:定位某一段的第一行p::first-line

##### 21. X:nth-child(n)
nth-child接受一个整形参数，然后它不是从0开始的。如果你想获取第二个元素那么你传的值就是li:nth-child(2).

##### 22. X:nth-last-child
它是从结尾处开始的，倒回去的。

##### 23. X:nth-of-type(n)
- 曾几何时，我们不想去选择子节点，而是想根据元素的类型来进行选择。
- 想象一下有5个ul标签。如果你只想对其中的第三个进行修饰，而且你也不想使用id属性，那你就可以使用nth-of-type(n)伪类来实现了：ul：nth-of-type(3)


##### 24. nth-last-of-type(n)

##### 25. X:first-child

##### 26. X:last-child

##### 27. X:only-child
它允许你获取到那些只有一个子标签的父标签。

##### 28. X:only-of-type
它会定位某标签只有一个子标签的目标。

##### 29. X:first-of-type
first-of-type伪类可以选择指定标签的第一个兄弟标签。

#### 伪元素选择器

- CSS 伪元素用于将特殊的效果添加到某些选择器

选择器 | 作用 | 栗子
---|---|---
x::after | 在元素x的内容前面插入新内容 | a:after
x::before | 在元素x的内容后面插入新内容 | a:before
x::first-line | 为某个元素的第一行文字使用样式 | p:first-line
x::first-letter | 为某个元素中的文字的首字母或第一个字使用样式 | p:first-letter
x::selection | 给光标选中的元素x添加样式 | input:selection

