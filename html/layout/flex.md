# Flex

## Flex布局：
- 设为 Flex 布局以后，子元素的float、clear和vertical-align属性将失效。

### 一.基本概念：
![Flex基本概念](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)
- 采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。
- 它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。
- 容器默认存在两根轴：
    1. 水平的主轴（main axis）
    2. 垂直的交叉轴（cross axis）。
- 主轴的开始位置（与边框的交叉点）叫做main start，
- 结束位置叫做main end；
- 交叉轴的开始位置叫做cross start，
- 结束位置叫做cross end。
<!-- more -->

### 二.容器的属性：
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

#### 2.1：flex-direction属性：决定主轴的方向（即项目的排列方向）。

```
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}

row（默认值）：主轴为水平方向，起点在左端。
row-reverse：主轴为水平方向，起点在右端。
column：主轴为垂直方向，起点在上沿。
column-reverse：主轴为垂直方向，起点在下沿。
```
![flex-direction](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)

#### 2.2：flex-wrap属性：默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。

```
    .box{
      flex-wrap: nowrap | wrap | wrap-reverse;
    }

nowrap（默认）：不换行。
wrap：换行，第一行在上方。
wrap-reverse：换行，第一行在下方。
```
![flex-wrap](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071006.png)

#### 2.3：flex-flow属性:flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

```
box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```
#### 2.4：justify-content属性:justify-content属性定义了项目在主轴上的对齐方式。

```
    .box {
      justify-content: flex-start | flex-end | center | space-between | space-around;
    }
    

        flex-start（默认值）：左对齐
        flex-end：右对齐
        center： 居中
        space-between：两端对齐，项目之间的间隔都相等。
        space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

```
![justify-content](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)

#### 2.5：align-items属性:align-items属性定义项目在交叉轴上如何对齐。

```
    
    .box {
      align-items: flex-start | flex-end | center | baseline | stretch;
    }

        flex-start：交叉轴的起点对齐。
        flex-end：交叉轴的终点对齐。
        center：交叉轴的中点对齐。
        baseline: 项目的第一行文字的基线对齐。
        stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

```
![align-items](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071011.png)

#### 2.6：align-content属性:align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

```
    .box {
      align-content: flex-start | flex-end | center | space-between | space-around | stretch;
    }

        flex-start：与交叉轴的起点对齐。
        flex-end：与交叉轴的终点对齐。
        center：与交叉轴的中点对齐。
        space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
        space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
        stretch（默认值）：轴线占满整个交叉轴。
```
![align-content](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)


### 三.项目的属性


- order
- flex-grow
- flex-shrink
- flex-basis
- flex
- align-self

#### 3.1: order属性:order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

```
    .item {
      order: <integer>;
    }
```
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)

#### 3.2: flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

```
    .item {
      flex-grow: <number>; /* default 0 */
    }
```

![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)

#### 3.3: flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。


```css
<!--如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。-->

<!--负值对该属性无效-->
    .item {
      flex-shrink: <number>; /* default 1 */
    }
```
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071015.jpg)

#### 3.4: flex-basis属性: 定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。


```css
.item {
  flex-basis: <length> | auto; /* default auto */
}
```

#### 3.5: flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

```css
<!--该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。-->
    .item {
      flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    }
```

#### 3.6: align-self属性:允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```css
    .item {
      align-self: auto | flex-start | flex-end | center | baseline | stretch;
    }
```
![image](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)