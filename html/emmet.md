## 1.初始化：

```html
<!-- html:5  -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>

</body>
</html>
```
## 2.元素：可以用任何元素名字来创建标签

```html
div -> <div></div>
```
## 3.嵌套操作
- child：>
```html
<!--使用>符号，将大于号右面元素嵌套在左面的元素之中。-->
<!-- div>ul>li -->
->
<div>
    <ul>
        <li></li>
    </ul>
</div>
```
- Sibling: +

```html
<!--使用+符号，使两者成为兄弟元素。-->
div + p
->
<div></div>
<p></p>
```
- Climb-up: ^

```html
<!--使用^，可以让元素在DOM中向上升一级。-->
div+div>p>span^p
->
<div></div>
<div>
    <p><span></span></p>
    <p></p>
</div>
<!--多个^,可以升多级。-->
```
- multiplication:*

```html
<!--用*可以定义需要创建多少次元素。-->
ul>li*5
->
<ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
</ul>
```

- Grouping:()

```html
<!--在复杂的缩写中，使用()将同一个父元素的元素连在一起。-->
(div>dl>(dt+dd)*3)+footer>p
->
<div>
    <dl>
        <dt></dt>
        <dd></dd>
        <dt></dt>
        <dd></dd>
        <dt></dt>
        <dd></dd>
    </dl>
</div>
<footer>
    <p></p>
</footer>
```

## 4.属性操作：
- ID和Class：同css一样，用#表示ID，.表示类。
```html
div#header+div.page
->
<div id="header"></div>
<div class="page"></div>
```
- 定制属性：使用[attr]添加你所想要的属性

```html
td[title="hello world" colspan=3]
->
<td title="Hello world!" colspan="3"></td>
```
- 项目编号：$-->使用*可以重复元素，使用$对其进行编号。

```html
ul>li.item$*5
->
<ul>
    <li class="item1"></li>
    <li class="item2"></li>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
</ul>

<!--也可以用多重$，用零填补不够的数字。-->
ul>li.item$$*5
->
<ul>
        <li class="item01"></li>
        <li class="item02"></li>
        <li class="item03"></li>
        <li class="item04"></li>
        <li class="item05"></li>
</ul>

<!--用@可以改变编号的顺序或开始的数字 
    @后添加-，递减排序
    @后加数字，改变开始的数字
-->
ul>li.item$@-*5
->
<ul>
    <li class="item5"></li>
    <li class="item4"></li>
    <li class="item3"></li>
    <li class="item2"></li>
    <li class="item1"></li>
</ul>

ul>li.item$@3*5
->
<ul>
    <li class="item3"></li>
    <li class="item4"></li>
    <li class="item5"></li>
    <li class="item6"></li>
    <li class="item7"></li>
</ul>

ul>li.item$@-3*5
->
<ul>
    <li class="item7"></li>
    <li class="item6"></li>
    <li class="item5"></li>
    <li class="item4"></li>
    <li class="item3"></li>
</ul>
```
- Text:{}  -->元素后加{}，就可以给元素添加文本值。
```html
a{Click me}
->
<a href="">Click me</a>

<!--注意{}的位置-->
p>{Click }+a{here}+{ to continue}
->
<p>Click <a href="">here</a> to continue</p>
```

## 5.CSS
1. 使用整数的缩写，会自动在后面添加px单位
```css
m10 -> margin:10px;
m10-20 -> margin:10px 20px;
m-10--20 -> margin:-10px -20px;
```

2. 使用浮点值的缩写,会自动在后面添加em单位
```css
m1.5 -> margin:1.5em;
```

3. 使用字母字符，就会自动明确单位
```css
m1.5ex -> margin:1.5ex;
```

4. 如果已经明确单位了，就不需要使用连字符了
```css
m10ex20em -> margin:10ex 20em;
m10ex-5 -> margin:10ex -5px;
```
5.值的别名：
```css
p -> %
e -> em
x -> ex
```

6.颜色：

```css
c#3 -> color:#333;
bd5#0s -> border:5px #000 solid;
#1 -> #11111
#e0 -> #e0e0e0
#fc0 -> #ffcc00
```
7.无单位属性：

```css
lh2 -> line-height: 2;
fw400 -> font-weight: 400;
```
8.供应商前缀：属性前加-，会自动添加供应商前缀，
```css
-bdrs -> 
        -webkit-border-radius: ;
        -moz-border-radius: ;
        -ms-border-radius: ;
        -o-border-radius: ;
        border-radius: ;
    <!--w: webkit-->
    <!--m: moz-->
    <!--s: ms-->
    <!--o: o-->
-wm-bdrs -> 
    -webkit-border-radius: ;
    -moz-border-radius: ;
```
9.渐变：使用lg(...)，就会自动添加渐变属性

```css
lg(left,#0,top,black) 
-> 
background-image: -webkit-linear-gradient(left, #0, top, black);
background-image: -o-linear-gradient(left, #0, top, black);
background-image: linear-gradient(to right, #0, top, black);
```
