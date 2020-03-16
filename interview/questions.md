## HTML

## CSS

### 1、解释css sprites ，如何使用？

- CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。

- CSS Sprites为一些大型的网站节约了带宽，让提高了用户的加载速度和用户体验，不需要加载更多的图片

## JS

### 1、如何用原生js给一个按钮绑定两个onclick事件？

- addEventListener

```js
//事件监听 绑定多个事件
var btn = document.getElementById("btn");
btn.addEventListener("click",hello1);
btn.addEventListener("click",hello2);
function hello1(){
 alert("hello 1");
}
function hello2(){
 alert("hello 2");
}
```

### 2、拖拽会用到哪些事件？

- dragstart:拖拽开始时在被拖拽元素上触发此事件,监听器需要设置拖拽所需数据,从操作系统拖拽文件到浏览器时不触发此事件.

- dragenter:拖拽鼠标进入元素时在该元素上触发,用于给拖放元素设置视觉反馈,如高亮

- dragover:拖拽时鼠标在目标元素上移动时触发.监听器通过阻止浏览器默认行为设置元素为可拖放元素.

- dragleave:拖拽时鼠标移出目标元素时在目标元素上触发.此时监听器可以取消掉前面设置的视觉效果.

- drag:拖拽期间在被拖拽元素上连续触发

- drop:鼠标在拖放目标上释放时,在拖放目标上触发.此时监听器需要收集数据并且执行所需操。如果是从操作系统拖放文件到浏览器,需要取消浏览器默认行为.

- dragend:鼠标在拖放目标上释放时,在拖拽元素上触发.将元素从浏览器拖放到操作系统时不会触发此事件.

### 3、document.write和innerHTML的区别？

- document.write是直接写入到页面的内容流，如果在写之前没有调用document.open, 浏览器会自动调用open。每次写完关闭之后重新调用该函数，会导致页面被重写。

- innerHTML则是DOM页面元素的一个属性，代表该元素的html内容。你可以精确到某一个具体的元素来进行更改。如果想修改document的内容，则需要修改document.documentElement.innerElement。

- innerHTML将内容写入某个DOM节点，不会导致页面全部重绘

- innerHTML很多情况下都优于document.write，其原因在于其允许更精确的控制要刷新页面的那一个部分。

### 4、什么是ajax? ajax的步骤？

- ajax(异步javascript xml) 能够刷新局部网页数据而不是重新加载整个网页。

- 如何使用ajax?

- 第一步，创建xmlhttprequest对象，var xmlhttp =new XMLHttpRequest（);XMLHttpRequest对象用来和服务器交换数据。

```js
var xhttp;
if (window.XMLHttpRequest) {
//现代主流浏览器
xhttp = new XMLHttpRequest();
} else {
// 针对浏览器，比如IE5或IE6
xhttp = new ActiveXObject("Microsoft.XMLHTTP");
}
```

- 第二步，使用xmlhttprequest对象的open（）和send（）方法发送资源请求给服务器。

- 第三步，使用xmlhttprequest对象的responseText或responseXML属性获得服务器的响应。

- 第四步，onreadystatechange函数，当发送请求到服务器，我们想要服务器响应执行一些功能就需要使用onreadystatechange函数，每次xmlhttprequest对象的readyState发生改变都会触发onreadystatechange函数。


### 5、xml和json的区别？

-  JSON相对于XML来讲，数据的体积小，传递的速度更快些

-  JSON与JavaScript的交互更加方便，更容易解析处理，更好的数据交互

-  XML对数据描述性比较好；

-  JSON的速度要远远快于XML；

### 6、 js有几种数据类型，其中基本数据类型有哪些？

- 五种基本类型: Undefined、Null、Boolean、Number和String。

- 引用类型: Object、Array和Function。

### 7、undefined和null的区别？

- null： Null类型，代表“空值”，代表一个空对象指针，使用typeof运算得到 “object”，所以你可以认为它是一个特殊的对象值。

- undefined： Undefined类型，当一个声明了一个变量未初始化时，得到的就是undefined。

- null是javascript的关键字，可以认为是对象类型，它是一个空对象指针，和其它语言一样都是代表“空值”，不过 undefined 却是javascript才有的。

- undefined是在ECMAScript第三版引入的，为了区分空指针对象和未初始化的变量，它是一个预定义的全局变量。没有返回值的函数返回为undefined，

- 没有实参的形参也是undefined。

- javaScript权威指南：
    1. null 和 undefined 都表示“值的空缺”，你可以认为undefined是表示系统级的、
    2. 出乎意料的或类似错误的值的空缺，而null是表示程序级的、正常的或在意料之中的值的空缺

### 8、JS哪些操作会造成内存泄露？

（1）意外的全局变量引起的内存泄露。
```js
function leak(){  
  leak="xxx";//leak成为一个全局变量，不会被回收  
}
```

（2）闭包引起的内存泄露。

（3）没有清理的DOM元素引用。

（4）被遗忘的定时器或者回调 

（5）子元素存在引起的内存泄露。

### 9、怎样添加、移除、移动、复制、创建和查找节点？

（1）创建新节点
- createDocumentFragment() //创建一个DOM片段
- createElement() //创建一个具体的元素
- createTextNode() //创建一个文本节点

（2）添加、移除、替换、插入
- appendChild() //添加
- removeChild() //移除
- replaceChild() //替换
- insertBefore() //插入

（3）查找
- getElementsByTagName() //通过标签名称
- getElementsByName() //通过元素的Name属性的值
- getElementById() //通过元素Id，唯一性

### 10、$(document).ready()方法和window.onload有什么区别？

(1)、window.onload方法是在网页中所有的元素(包括元素的所有关联文件)完全加载到浏览器后才执行的。

(2)、$(document).ready() 方法可以在DOM载入就绪时就对其进行操纵，并调用执行绑定的函数。

## Browser(浏览器)

### 1、请描述一下 cookies sessionStorage和localstorage区别？

- 相同点：都存储在客户端

- 不同点：

不同点 | cookie | sessionStorage | localStorage
---|---|---|---
存储大小|cookie数据大小不能超过4k|sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大|-
有效时间|设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭 | 数据在当前浏览器窗口关闭后自动删除|存储持久数据，浏览器关闭后数据不丢失除非主动删除数据；
数据与服务器之间的交互方式|数据会自动的传递到服务器，服务器端也可以写cookie到客户端|sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存|-

### 2、优雅降级和渐进增强？

- 渐进增强（Progressive Enhancement）：一开始就针对低版本浏览器进行构建页面，完成基本的功能，然后再针对高级浏览器进行效果、交互、追加功能达到更好的体验。

- 优雅降级（Graceful Degradation）：一开始就构建站点的完整功能，然后针对浏览器测试和修复。比如一开始使用 CSS3 的特性构建了一个应用，然后逐步针对各大浏览器进行 hack 使其可以在低版本浏览器上正常浏览。

- 其实渐进增强和优雅降级并非什么新概念，只是旧的概念换了一个新的说法。在传统软件开发中，经常会提到向上兼容和向下兼容的概念。渐进增强相当于向上兼容，而优雅降级相当于向下兼容。

### 3、浏览器是如何渲染页面的？

1.解析HTML文件，创建DOM树。**
**自上而下，遇到任何样式（link、style）与脚本（script）都会阻塞（外部样式不阻塞后续外部脚本的加载）。

2.解析CSS。优先级：浏览器默认设置<用户设置<外部样式<内联样式<HTML中的style样式。

3.将CSS与DOM合并，构建渲染树（Render Tree）。

4.布局和绘制，重绘（repaint）和重排（reflow）。**

### 4、从输入url到显示页面，都经历了什么？

1、首先，在浏览器地址栏中输入url。
2、浏览器先查看浏览器缓存-系统缓存-路由器缓存，如果缓存中有，会直接在屏幕中显示页面内容。若没有，则跳到第三步操作。
3、在发送http请求前，需要域名解析(DNS解析)(DNS（域名系统，Domain Name System）是互联网的一项核心服务，它作为可以将域名和IP地址相互映射的一个分布式数据库，能够使人更方便的访问互联网，而不用去记住IP地址。)，解析获取相应的IP地址。
4、浏览器向服务器发起tcp连接，与浏览器建立tcp三次握手。（TCP即传输控制协议。TCP连接是互联网连接协议集的一种。）
5、握手成功后，浏览器向服务器发送http请求，请求数据包。
6、服务器处理收到的请求，将数据返回至浏览器。
7、浏览器收到HTTP响应。
8、读取页面内容，浏览器渲染，解析html源码。
9、生成Dom树、解析css样式、js交互。
10、客户端和服务器交互。
11、ajax查询。