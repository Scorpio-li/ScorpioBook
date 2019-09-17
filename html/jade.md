## 1.模式：开始标签+(类名/Id)+ 空格 + 内容:空格不能省略

```html
eg:span.abc span content = <span class="abc">span content</span>
```
## 2.嵌套关系：由缩进决定

```html
eg:div 
     p content = <div><p>content</p></div>
```
<!-- more -->
## 3. 件的包含include和扩展extends:
- 分别说明:include 较符合正常思维，什么地方缺某部分包含进来即
可;extend则使用先给出整体，再替换局部的模式。

```jade
//- index.jade
doctype html
html
        include ./layout/header.jade
        body
        h1 include demo
        p content
include ./layout/footer.jade

extends的例子
//- layout.jade
doctype html
html
        head
                block title
                title Default Title
        body
                block content
//- index.jade
extends ./layout/layout.jade
//-进行替换 
block title
        title New Title
block content
        h1 extends demo
        p content
```