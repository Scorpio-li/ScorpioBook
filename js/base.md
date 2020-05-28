# JS 基础

## 浏览器

### 一、浏览器分类

1. 以谷歌浏览器webkit内核为主（V8引擎）

    - 谷歌浏览器 Chrome

    - 苹果浏览器 Safari

    - 国产浏览器
        
        - 360普通浏览器
        
        - 360极速浏览器
        
        - 猎豹浏览器
        
        - 搜狗浏览器
        
        - QQ浏览器
        
        - UC浏览器
        
        - ... 欧朋浏览器 Opera （v14版本时候）

2. Gecko内核
    
    - 火狐浏览器 Firefox

3. Trident内核
    
    - IE浏览器
    
    - IE6~8
    
    - IE9~IE11
    
    - IE Edge

### 二、开发者工具

> 打开开发者工具：F12 / FN+F12 （再或者浏览器页面 -> 右键 ->检查）

- Elements 包含了当前页面中所有的结构和样式，基于它可以快速查看和调整页面的样式和结构等

- Console 控制台，在JS中，我们可以向控制台输出一些内容，来进行项目的调试；如果项目程序出现问题，也可以在控制台查看报错信息；也可以在控制台编写代码，做一些测试...

- Network 包含了当前页面所有向服务器发送的HTTP请求信息，一般用于前后端数据交互中的BUG调试以及页面中的性能优化

- Sources 包含了当前项目的原代码

- Application 可以看到本地存储的信息(Cookie/LocalStorage/SessionStorage...)以及当前网站中所有加载的图片等信息（抓取一些图片下来）

- ...

- 开启手机模拟器 Toggle Device Toolbar

### 三、Web页面组成

- HTML 搭建页面结构

- CSS 编写页面样式

- JS 完成人机交互效果
    
    - 基本的人机交互效果
    
    - 页面中具体效果的实现
    
    - 页面中动态数据的获取和绑定
    
    - 可能会操作浏览器的一些功能

> JS是用来操作DOM和操作浏览器的

## JS 初识

### 一、JS组成的三部分

- ECMAScript（ES3 / ES6~9） 定义了JS的语法规范：定义了语言本身的变量、数据值、操作语句、内存管理...等内容

- DOM（document object model）文档对象模型：提供对应的属性和方法，可以让JS操作页面中的DOM元素

- BOM（browser object model）浏览器对象模型：提供操作浏览器的属性和方法

> 注意：当代项目开发，一般都是基于Vue/React完成的，基于这两个框架，我们已经不去操作DOM了，我们操作数据，由框架本身帮助我们完成DOM的操作

### 二、JS中的变量 variable [ˈveəriəbl]

> 变量：可变的量（其存储的值是可变的），设置一个变量（起个名字），让其代表和指向某一个具体的值

#### 1.JS中创建变量的几种方式

- ES3：var

- ES6：let 、const

- function 创建函数

- class 创建一个类

- import / require 基于ES6Module或者Common.js规范导入模块

```js
// 1.基于VAR创建
var n = 10;
var m;
console.log(n, m); //=>10 undefined

// 2.基于ES6中的LET创建
let a = 100;
a = 200;
console.log(a); //=>200

// 3.基于ES6中的CONST创建(基于CONST定义的变量一般也被成为常量)；
const b = 1000;
b = 2000;
console.log(b); //=>Uncaught TypeError: Assignment to constant variable.

// 4.创建一个函数
function func() {}
console.log(func);

// 5.创建一个类
class Parent {}
console.log(Parent);

// 6.基于模块规范来导入具体的某个模块
import axios from './axios';
let axios = require('./axios');
```

#### 2.变量命名的规范

- 严格遵循大小写

```js
//=>编写代码的时候一定要区分大小写问题
let Test = 100;
console.log(test); //=>Uncaught ReferenceError: test is not defined
```

- 使用驼峰命名法

> 由有意义英文组成一个名字，第一个单词首字母小写，其余每一个有意义的单词首字母大写

```js
let studentInfomation = {
	name: '好好学习'
};
let studentInfo = {};

//=>项目中常见的有特殊含义的端词组
add / insert / create  新增/插入/创建
del / delete / remove  删除/移除
update 修改
select / query / get  查询/获取
info 信息
...
```

- 命名规则：使用 “$、_、英文字母、数字” 命名

> 数字不能作为开头

```js
// 基于$开头：一般代表使用JQ或者其它使用$的类库获取的内容
let $box;
// 基于_开头：一般代表是全局或者公共的变量
let _box = {};
// 基于数字区分相似名称的变量
let box1 = 10;
let box2 = 20;
// 数字不能作为开头
// let 2box = 10;
// 想要分隔单词，可以使用_或者驼峰，但是不能是-
// let box-list;
let box_list;
let boxList;
// 虽然不会报错，但是强烈不推荐
let 盒子 = 100;
console.log(盒子);
```

- 不能使用关键字和保留字

> 关键字：在JS中有特殊含义的 保留字：未来可能会成为关键字的

### JS中的数据类型

#### 基本数据类型（值类型 / 原始值）

- 数字 number

- 字符串 string

- 布尔 boolean

- 空对象指针 null

- 未定义 undefined

- ES6新增的唯一值类型 symbol

#### 引用数据类型

- 对象数据类型 object

    - 普通对象 {}

    - 数组对象 []

    - 正则对象 /^$/

    - 日期对象 new Date

    - 数学函数对象 Math
    
    - ...

- 函数数据类型 function

```js
// number数字类型
	let n = 10;
	n = 10.5;
	n = -10;
	n = 0;
	n = NaN; //=>NaN：not a number 非有效数字
	n = Infinity; //=>正/负无穷大  -Infinity   [ɪnˈfɪnəti]

// string字符串：基于单引号、双引号、反引号（TAB上面的撇）包起来的都是字符串
	let str = '';
	str = '19';
	str = "好好学习";
	str = `我是ES6中新增的模板字符串，有助于字符串的拼接`;
	str = '[object Object]';

// boolean布尔：true / false
	let boo = true;
	boo = false;

// 空
	let nu = null;
	nu = undefined;
	let un; //=>默认值就是undefined

// Symbol：每一个Symbol()都是一个唯一值
	let x = Symbol('珠峰');
	let y = Symbol('珠峰');
	console.log(x == y); //=>false

// object普通对象：大括号包起来，里面有零到多组属性名和属性值（键值对），这些属性名和属性值可以描述当前对象的特征（键:值，多组键值对用逗号分隔）
	let obj = {
		name: '好好学习',
		age: 10,
		teachers: 30
	};

// Array数组对象：中括号包起来，逗号分隔数组中每一项的值（每一项的值可以是任意类型）
	let arr = [10, '字符串', true, null];

// RegExp正则对象：两个斜杠包起来一大堆你看不懂的符号就是正则 O(∩_∩)O哈哈~
	let reg = /$[+-]?(\d|([0-9]\d+))(\.\d+)?^/;

// function函数
	function func(x, y) {
		let total = x + y;
		return total;
	}
	
// ES6中的 Arrow Function 箭头函数
	let fn = () => {

	};
```

## JS中的三大类输出方式

> 说到输出方式我们主要分为三大类：控制台输出类、window提示框类、页面插入类；接下来我们主要介绍几种常用的

### 一、console：控制台输出类

> 控制在浏览器控制台输出的

#### 1、console.log

- 定义：控制台输出

- 特点：输出任意数据类型的数据，控制台展示的也是对应的数据类型

- 举例：

```js
let aa = {name: 'xiaozhima',age:18}
let bb = {name: 'lingling'}
console.log(aa,bb);
console.log({
    name: 'xiaozhima',
    age: '18'
})
```

#### 2、console.dir

- 定义：输出一个对象或者一个值的详细信息

```js
let aa = { name: 'xiaozhima', age: 18 }
console.dir(aa);
console.dir({
    name: 'xiaozhima',
    age: '18'
})
```

- 与console.log的区别：console.log可以一次性输出多个值，但是dir不可以

```js
let aa = { name: 'xiaozhima', age: 18 }
let bb = { name: 'lingling' }
console.log(aa, bb);

let aa = { name: 'xiaozhima', age: 18 }
let bb = { name: 'lingling' }
console.dir(aa, bb);//==>第二个变量未识别
```

- 实际情况中经常使用console.dir输出一个方法或一个数据类型的详细信息

#### 3、console.warn

- 定义：以警告的方式输出

```js
console.warn(‘当前操作不规范’)
```

#### 4、console.table

- 定义：把多维的JSON数据以表格形式输出

```js
let aa = { name: 'xiaozhima', age: 18 }
console.table(aa)
```

#### 5、console.time / console.timeEnd

- 定义：计算出time / timeEnd 中间所有程序执行所消耗的时间（预估时间，受到当前电脑性能的影响）

```js
console.time('AA');
for (let i = 0; i < 99999999; i++) {}
console.timeEnd('AA');
```


### 二、window提示框类

> 是在浏览器窗口中弹出一个提示框，提示框中输出指定的信息

#### 1、alert

- 特点：
    
    1. 需要等到 alert 弹出框，点击确定关闭后，后面的代码才会执行（alert 会阻碍主线程的渲染）
    
    2. alert 弹出的内容都会默认转换为字符串（调用 toString）

```js
alert('今天大家都很帅！');
console.log(100);
alert([10, 20, 30]); //=>数组转换为字符串的结果 "10,20,30"
alert({name:'小芝麻'}); //=>普通对象转换为字符串的结果 "[object Object]"
```

#### 2、confirm

- 特点：创建一个变量，用来接收用户选择的结果
    
    - 用户点击确定返回true
    
    - 用户点击取消返回false

```js
let flag = confirm('今天大家都好好学了吗？');
console.log(flag);
```

#### 3、prompt

- 特点：
    
    - 点击的是取消返回结果是null
    
    - 点击的是确定，会把用户输入的原因信息返回

```js
let reason = prompt('确定要删除此信息吗？');
console.log(reason);
```

### 三、页面插入类

> 向页面指定容器中插入内容

#### 1、document.write（不常用）

- 定义：在页面中直接写入

- 特点：和 alert 一样，写入的内容最后都会转换为字符串，然后写入

#### 2、innerHTML

- 特点：

    - 插入的信息也会变成字符串

    - 基于这种方式会把之前容器中的内容给覆盖掉，想要追加，则采用+=的方式

```js
box.innerHTML = 'xiaozhima';//==>会覆盖原始的所有内容
box.innerHTML += 'xiaozhima';//==>在原始内容上继续增加
```

#### 3、innerText（与innerHTML基本相同）

- 与innerHTML唯一的区别：

    - innerHTML 能够把标签文本进行识别和渲染

    - innerText 会把所有内容都当作普通的文本

#### 4、value

- 定义：给页面中的文本框赋值

```js
// 给页面中的文本框赋值
let userName = document.getElementById('userName');
userName.value = "我是在JS中插入的内容";
```