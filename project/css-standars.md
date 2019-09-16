# 一. 什么是BEM
BEM(Block Element Modifier) 是一种命名CSS class的模式，使用这种模式可以让 CSS 代码更加利于维护。标准的 BEM 写法是 .block-name__element-name--modifier-name。

## 1. Block

- 页面上逻辑和功能独立的，可复用的组件，可以嵌套并相互交互，但在语义上它们保持平等，可以存在页面上不同的位置或不同项目中，保持样式不变

- 可以使用字母，数字，连字符进行命名，任何html元素都可以成为一个block，不依赖于页面上的其他block或者element。

```html
<header class="header"></header>
```
```css
.header {
  color: #333;
  background: #f5f5f5;
}
```

## 2. Element

- 组成块的一部分，内部的任何元素都与块有关联，不能在块的外部使用。

```html
<article class="article">
  <h2 class="article__title"></h2>
  <p class="article__content"></p>
</article>
```

```css
.article {
  padding: 12px;
}

.article__title {
  font-size: 1rem;
}

.article__content {
   font-size: .9rem;
}
```

## 3. Modifier

- 用来表示块或者元素的状态，外观或者行为，不必须，可以选择使用。

```html
<button class="btn btn--disabled"></button>
```

```css
.btn {
  color:  #333;
  background-color: #fff;
}

.btn--disabled {
  color: #fff;
  background-color: #6c757d;
}
```

# 二. 常用CSS class名

- 包裹类： container, wrapper, outer, inner, box, header, footer, main, content, aside, page, section, block

- 状态类： primary, secondary, success, danger, warning, info, error, Link, light, dark, disabled, active, checked, loading

- 尺寸类： large, middle, small, bigger, smaller

- 组件类： card, list, picture, carousel, swiper, menu, navs, badge, hint, modal, dialog

- 位置类： first, last, current, prev, next, forward, back

- 文本类： title, desc, content, date, author, category，label，tag

- 人物类： avatar, name, age, post, intro