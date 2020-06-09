#原生JS

## JS 基础

### 浏览器

#### 一、浏览器分类

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

#### 二、开发者工具

> 打开开发者工具：F12 / FN+F12 （再或者浏览器页面 -> 右键 ->检查）

- Elements 包含了当前页面中所有的结构和样式，基于它可以快速查看和调整页面的样式和结构等

- Console 控制台，在JS中，我们可以向控制台输出一些内容，来进行项目的调试；如果项目程序出现问题，也可以在控制台查看报错信息；也可以在控制台编写代码，做一些测试...

- Network 包含了当前页面所有向服务器发送的HTTP请求信息，一般用于前后端数据交互中的BUG调试以及页面中的性能优化

- Sources 包含了当前项目的原代码

- Application 可以看到本地存储的信息(Cookie/LocalStorage/SessionStorage...)以及当前网站中所有加载的图片等信息（抓取一些图片下来）

- ...

- 开启手机模拟器 Toggle Device Toolbar

#### 三、Web页面组成

- HTML 搭建页面结构

- CSS 编写页面样式

- JS 完成人机交互效果
    
    - 基本的人机交互效果
    
    - 页面中具体效果的实现
    
    - 页面中动态数据的获取和绑定
    
    - 可能会操作浏览器的一些功能

> JS是用来操作DOM和操作浏览器的

### JS 初识

#### 一、JS组成的三部分

- ECMAScript（ES3 / ES6~9） 定义了JS的语法规范：定义了语言本身的变量、数据值、操作语句、内存管理...等内容

- DOM（document object model）文档对象模型：提供对应的属性和方法，可以让JS操作页面中的DOM元素

- BOM（browser object model）浏览器对象模型：提供操作浏览器的属性和方法

> 注意：当代项目开发，一般都是基于Vue/React完成的，基于这两个框架，我们已经不去操作DOM了，我们操作数据，由框架本身帮助我们完成DOM的操作

#### 二、JS中的变量 variable [ˈveəriəbl]

> 变量：可变的量（其存储的值是可变的），设置一个变量（起个名字），让其代表和指向某一个具体的值

##### 1.JS中创建变量的几种方式

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

##### 2.变量命名的规范

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

#### JS中的数据类型

##### 基本数据类型（值类型 / 原始值）

- 数字 number

- 字符串 string

- 布尔 boolean

- 空对象指针 null

- 未定义 undefined

- ES6新增的唯一值类型 symbol

##### 引用数据类型

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

### JS中的三大类输出方式

> 说到输出方式我们主要分为三大类：控制台输出类、window提示框类、页面插入类；接下来我们主要介绍几种常用的

#### 一、console：控制台输出类

> 控制在浏览器控制台输出的

##### 1、console.log

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

##### 2、console.dir

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

##### 3、console.warn

- 定义：以警告的方式输出

```js
console.warn(‘当前操作不规范’)
```

##### 4、console.table

- 定义：把多维的JSON数据以表格形式输出

```js
let aa = { name: 'xiaozhima', age: 18 }
console.table(aa)
```

##### 5、console.time / console.timeEnd

- 定义：计算出time / timeEnd 中间所有程序执行所消耗的时间（预估时间，受到当前电脑性能的影响）

```js
console.time('AA');
for (let i = 0; i < 99999999; i++) {}
console.timeEnd('AA');
```


#### 二、window提示框类

> 是在浏览器窗口中弹出一个提示框，提示框中输出指定的信息

##### 1、alert

- 特点：
    
    1. 需要等到 alert 弹出框，点击确定关闭后，后面的代码才会执行（alert 会阻碍主线程的渲染）
    
    2. alert 弹出的内容都会默认转换为字符串（调用 toString）

```js
alert('今天大家都很帅！');
console.log(100);
alert([10, 20, 30]); //=>数组转换为字符串的结果 "10,20,30"
alert({name:'小芝麻'}); //=>普通对象转换为字符串的结果 "[object Object]"
```

##### 2、confirm

- 特点：创建一个变量，用来接收用户选择的结果
    
    - 用户点击确定返回true
    
    - 用户点击取消返回false

```js
let flag = confirm('今天大家都好好学了吗？');
console.log(flag);
```

##### 3、prompt

- 特点：
    
    - 点击的是取消返回结果是null
    
    - 点击的是确定，会把用户输入的原因信息返回

```js
let reason = prompt('确定要删除此信息吗？');
console.log(reason);
```

#### 三、页面插入类

> 向页面指定容器中插入内容

##### 1、document.write（不常用）

- 定义：在页面中直接写入

- 特点：和 alert 一样，写入的内容最后都会转换为字符串，然后写入

##### 2、innerHTML

- 特点：

    - 插入的信息也会变成字符串

    - 基于这种方式会把之前容器中的内容给覆盖掉，想要追加，则采用+=的方式

```js
box.innerHTML = 'xiaozhima';//==>会覆盖原始的所有内容
box.innerHTML += 'xiaozhima';//==>在原始内容上继续增加
```

##### 3、innerText（与innerHTML基本相同）

- 与innerHTML唯一的区别：

    - innerHTML 能够把标签文本进行识别和渲染

    - innerText 会把所有内容都当作普通的文本

##### 4、value

- 定义：给页面中的文本框赋值

```js
// 给页面中的文本框赋值
let userName = document.getElementById('userName');
userName.value = "我是在JS中插入的内容";
```

### 数据类型基础知识

> JS中的数据类型，是学习JS的基础，他主要分为两大类分别是：
>    - 基本数据类型和引用数据类型，基本数据类型又分为number、string、boolean、null、undefined、还有ES6新语法规范中的Symbol，BigInt
>    - 引用数据类型：对象(普通对象、数组对象、正则对象、Math、Date)、函数

#### 一、基本数据类型

> 按值操作

##### number

- 正数、负数、0

- NaN
    
    - not a number 不是一个有效数字，但是属于number类型的
    
    - NaN和任何值都不相等（包括自己本身）
    
    - NaN == NaN //=>false

- Infinity:无穷大的值，也是number类型的

###### 1、isNaN

定义：专业用来验证一个值是否为非有效数字

- 返回值

    - 有效数字：返回false

    - 非有效数字：返回true

```js
console.log(isNaN(1)); //=>false
console.log(isNaN(NaN)); //=>true
console.log(isNaN(Infinity)); //=>false
console.log(isNaN('AA')); //=>true
console.log(isNaN('12.5')); //=>false
console.log(isNaN('12.5px')); //=>true
console.log(isNaN([])); //=>false
console.log(isNaN([10])); //=>false
console.log(isNaN([10, 20])); //=>true
console.log(isNaN({})); //=>true
console.log(isNaN(null)); //=>false
console.log(isNaN(undefined)); //=>true
console.log(isNaN(Symbol(1))); //=>报错
```

> 在使用 isNaN 进行检测的时候，如果检测的值是非数字类型的值，则需要先把其转换为数字类型，然后在进行检测。

###### 2、把其它数据类型转换为数字类型

1) Number([value])

- 定义：是JS内置的转换方法，可以把其他数据类型“强制”转换为数字类型

- 1、字符串转数字

    - 只有都是有效数字字符的才能转换为具体的数字，一旦字符串中出现非有效数字字符，则结果为NaN
    
    - 空字符串转数字===>0

```js
console.log(Number('12')); //=>12
console.log(Number('12.5')); //=>12.5
console.log(Number('12px')); //=>NaN
console.log(Number('12.5.0')); //=>NaN
```

- 2、布尔转数字
    
    - true 转换为1
    
    - false 转换为 0
```js
console.log(Number(true)); //=>1
console.log(Number(false)); //=>0
```

- 3、把空转数字

    - null 转换为 0

    - undefined 转换为NaN
```js
console.log(Number(null)); //=>0
console.log(Number(undefined)); //=>NaN
```

- 4、Symbol 转数字
    
    - 不能把Symbol类型转换为数字，否则会报错
```js
console.log(Number(Symbol(13))); //=>Cannot convert a Symbol value to a number
```

- 5、对象转数字
    
    - 过程：
        
        - 1.先把obj转化为字符串 "[object Object]"
        
        - 2.把字符串转换为数字 Number("[object Object]")
    - 普通对象:
        ```js
        let obj={x:100};
        console.log(Number(obj)); //=>NaN
        ```
    - 数组对象：空数组转数字为 0
        ```js
        /*
        * 1.先把ARR转换为字符串： "10"
        * 2.在把"10"转换为数字：10
        */
        let arr = ["10"];
        console.log(Number(arr)); //=>10
        /*
        * 1.先把ARR转换为字符串： "10,20"
        * 2.在把"10,20"转换为数字：NaN
        */
        arr = ["10", "20"];
        console.log(Number(arr)); //=>NaN
        console.log(Number([])); //=>  []->''  Number('')->0
        console.log(Number(['AA'])); //=> ['AA']->'AA'  Number('AA')->NaN
        ```
    - 其余对象基本都是NaN

- 6、函数转数字: 结果都是NaN


2) parseInt([value])

- 定义：从字符串最左边开始查找，把找到的有效数字字符转换为数字，一直遇到一个非有效数字字符为止，则结束查找

- 原理：

    - 处理原理与Number不一样
    
    - 他们是把字符串转换为数字类型（如果处理的值不是字符串，需要先转换为字符串然后再去转换为number类型的）

3）parseFloat([value])

- 与 parseInt 区别

    - parseFloat 比 parseInt 多识别一位小数点

    ```js
    console.log(Number('12px')); //=>NaN
    console.log(parseInt('12px')); //=>12
    console.log(parseInt('12px24')); //=>12
    console.log(parseInt('width:12px')); //=>NaN
    console.log(parseInt('12.5px')); //=>12
    console.log(parseFloat('12.5px')); //=>12.5  parseFloat比parseInt多识别一个小数点

    console.log(Number(true)); //=>1
    console.log(parseInt(true)); //=>先把TRUE转换为字符串"TRUE"  parseInt('true') =>NaN
    console.log(parseInt(NaN)); //=>NaN
    console.log(Number(null)); //=>0
    console.log(parseInt(null)); //=> parseInt('null') =>NaN
    console.log(isNaN(Number(parseInt("0.8")))); //=>parseInt("0.8")->0   Number(0)->0  isNaN(0)->false

    console.log(Number('')); //=>0
    console.log(parseInt('')); //=>NaN
    ```


###### 3、方法

> 在Number这一大类中，有很多公用的方法，本次只列举两个较为常用的

1. toFixed()

- 语法：数字.toFixed(N)

- 定义：保留小数点后N位（最后的结果是一个字符串）

```js
let n = 3.1415926;
console.log(n.toFixed(2)); //=>"3.14"
```

2. MAX_SAFE_INTEGER

- 定义：最大安全数（js能够识别的最大整数）

- 数值：9007199254740991

- 注意：ES6中提供了一个新的数据类型 BigInt ，管理超过安全数值的数字

```js
console.log(Number.MAX_SAFE_INTEGER); //=>9007199254740991 最大安全数（JS能够有效识别的最大整数）
console.log(9007199254740992 == 9007199254740993); //=>true  应该是不一样的，但是超过了最大数值，JS无法精准计算
ES6中提供了一个新的数据类型 BigInt：管理超过安全数值的数字
console.log(BigInt(9007199254740992), BigInt(9007199254740993));
/* 
 * 基本数据类型
 *   number string boolean null undefined symbol  => BigInt新增的基本数据类型
 */
```

##### string

定义：在JS中，用单引号/双引号/反引号，包起来的都是字符串

###### 1、把其它数据类型转换为字符串类型：

- 方法：
    
    - String([value])
    
    - [value].toString()

- 隐式转换：
    
    - 字符串拼接时
    
    - 把对象转换为数字之前，先要转换为字符串

- 普通对象转字符串：“[object object]”

- 数组对象转换为字符串：“第一项，第二项，...”（用逗号分隔数组中的每一项）

###### 2、在JS中常用的数学运算

- %（膜）取余数

```js
console.log(7 % 3); //=>取余  1
```

- 减乘除：都是数学运算（如果遇到非数字类型，需要基于Number 把其强制转换为数字类型，然后进行运算）

- 加的作用：
    
    - 数学运算：
    
    - 字符串拼接：

###### 字符串拼接

- 定义：只要加号两边的任意一边出现字符串，则变为字符串拼接

- 注意：对象转数字时需要先转换为字符串，变为字符串之后则直接拼接，不再转为数字

- 例子：console.log(100 + true + 21.2 + null + undefined + 'Tencent' + [] + null + 9 + false)；//==>NaNTencentnull9false

```js
console.log(3 - "3px"); //=>NaN
console.log(3 + "3px"); //=>"33px"  字符串拼接
console.log(1 + "1"); //=>"11" 字符串拼接
console.log(1 + {}); //=>"1[object Object]"  在把{}转换为数字过程中，先把他转换为字符串"[object Object]"，此时右侧出现了字符串，则不再是数学运算，而是字符串拼接了
console.log(1 + []); //=>'1'
console.log([10] + true); //=>"10true"  在转换[10]到数字的过程中，先把其转换为字符串"10"，此时操作变为字符串拼接(和数学运算没关系了)
console.log(true + [10]); //=>"true10"
console.log(1 + true); //=>2

console.log(100 + true + 21.2 + null + undefined + "Tencent" + [] + null + 9 + false);
    100 + true => 101
    101 + 21.2 => 122.2
    122.2 + null => 122.2
    122.2 + undefined => NaN 
    NaN + "Tencent" => "NaNTencent"  字符串拼接（以后都是字符串拼接）
    "NaNTencent" + [] => "NaNTencent"
    "NaNTencent" + null => "NaNTencentnull"
    "NaNTencentnull" + 9 => "NaNTencentnull9"
    "NaNTencentnull9" + false => "NaNTencentnull9false"
```

ES6 中的模版字符串

- 反引号${}反引号：为了解决传统字符串拼接中的问题反引号${}反引号中存放变量或者其他的JS表达式即可

- let result = 反引号${year}年${mouth}月${day}日${hours}:${minutes}:${seconds}反引号

- 可以很简单的完成字符串拼接

```js
// ES6中的模板字符串就是为了解决传统字符串拼接中的问题（反引号 TAB上面的撇）：${}中存放变量或者其它的JS表达式即可，很简单的完成字符串拼接
	let result = `${year}年${month}月${day}日 ${hours}:${minutes}:${seconds}`;
	console.log(result);
```

```js
//从页面中获取一个元素拼接内容

let str = `<div class="box" id="box">
	<h2 class="title">哈哈</h2>
	    <ul class="item">
		${[10,20,30].map(item=>{
			return `<li>${item}</li>`;
		}).join('')}
	    </ul>
	</div>`;
	console.log(str); 
```

##### boolean


1、把其它数据类型转换为布尔类型

- 方法：
    
    - Boolean([value])
    
    - ![value] ： 把指定的值转换为布尔类型后取反
    
    - !![value] ： 取反再取反，相当于没有取反，只是把它转换为布尔类型值

- 规则

    - 只有 “0/NaN/null/undefined/空字符串” 最后是false，其余的都是true

```js
console.log(!!1); //=>true
console.log(!1); //=>false

console.log(!!-1); //=>true
console.log(!!0); //=>false
console.log(!!undefined); //=>false
console.log(!!Number('12px')); //=>Number('12px')->NaN  false
console.log(!![]); //=>true
console.log(!!''); //=>false
console.log(!!{}); //=>true
```

- 条件判断时：

```js
/* 条件判断中，每一个条件最后一定是true/false */
    if (1 == 1) {}
	if (1) {
		//=>写一个值，也是要把这个值转换为布尔，然后校验程序的真假
	}
	if (3 + '3px') {} //=>3 + '3px' =>'33px'  真
	if (3 - '3px') {} //=>3 - '3px' =>NaN   假
```

##### null 和undefined

- null 空对象指针

- undefined 的应用场景

1、声明了一个变量，但是没有赋值，这个变量就是undefined;

```js
var num;
console.log(num)===>undefined
```

2、我们在获取一个对象的属性名对应的属性值的时候，如果这个属性名在对象中没有，得到的这个值就是undefined

```js
var obj={name:"lili"};
    obj.name ====>"lili"
    obj.age====>undefined
```

3、如果函数里面有形参，咱们在执行函数的时候，并没有传参数，那么，在函数体中去打印这个形参，得到值就是undefined;

```js
function fn(n,m){
    console.log(n);====>undefined
 }
fn()
```

4、正常的一个函数里面return多少，那么这个执行函数最后的返回结果就是多少，如果没写return，（即此函数没有返回值），在执行函数的时候，返回值就是undefined;

```js
function fn2(){

}
var res=fn2()  =====>undefined;
```

#### Object

##### 一、定义

- 1、用键值对（key:value 俗称属性名和属性值）来描述一个对象的特征（每一个对象都是综合体，存在零到多组键值
- 对）；

- 2、{ key : value , ...} 每组键值对是key : value 的格式，多组键值对用逗号分隔；

- 3、key 不能是引用数据类型，value 可以是任何的数据类型

```js
let obj = {
	name: '张三',
	age: 25,
	sex: '男',
	score: [100, 98, 89],
	fn: function () {}
    };
console.log(obj);
```

##### 二、键值对

组成：

- 属性名：属性值

操作方式：

- 1、对象.属性名 = 属性值

- 2、对象[属性名] = 属性值

###### 1、获取

获取值：

1. 对象.属性名

    - 基于这种方法操作，属性名就是.后面的
    - 这种方式，属性名不能是数字


2. 对象[属性名]

    - 1、基于这种方式操作，需要保证属性名是一个值（字符串/数字/布尔都可以）
    - 2、如果不是值而是一个变量，它会把变量储存的值作为对象的属性名进行操作
    - 如果属性名是数字则只能用此方法

```js
let n = 100;
let obj = {
	1: 100
};
console.log(obj[1]);
console.log(obj.1); //=>Uncaught SyntaxError: missing ) after argument list 
基于点的方式操作有自己的局限性，属性名不能是数字的，不能 对象.数字属性，此时只能用 对象[数字属性]

console.log(obj[1]);
console.log(obj['1']); //=>其它非字符串格式作为属性名和字符串格式没啥区别

obj.n = 200; //=> {n:200}  n是属性名（数据格式是字符串）
obj['n'] = 200; //=> {n:200} 和上面的情况一样

obj[n] = 200; //=> {100:200} => obj[100]=200   
n本身是一个变量（n和'n'的区别：前者是一个变量，后者是一个字符串的值），它代表的是所存储的值100（是一个数字格式）

obj[m] = 200; //=>Uncaught ReferenceError: m is not defined 
m这个变量没有被定义

obj[true] = 300; //=>{true:300}
obj[undefined] = 400; //=>{undefined:400}

console.log(obj);
```

- 获取所有属性名 - Object.keys(对象)：返回结果是包含所有属性名的数组

```js
let obj = {
    sex: 0
};
//============================
1）获取指定属性名的属性值
    console.log(obj.sex); //=>0
    console.log(obj['sex']); //=>0
2）如果指定的属性不存在，获取到的属性值是undefined（不会报错）
    console.log(obj['age']); //=>undefined
3）获取当前对象中所有的属性名：返回结果是包含所有属性名的数组
    console.log(Object.keys(obj)); //=>["sex"]
```

###### 2、增加 | 修改

原理：对象的属性名（键）是不允许重复的

- 之前没有这个属性则为新增

- 之前有这个属性名，则是修改对应的属性值

```js
let obj = {
    sex: 0
};
//============================
obj.name = '张三';//=> 新增
obj['name'] = "李四";//=> 修改  因为此时obj中已经有name：‘张三’存在了，所以此次操作为修改
```

###### 3、删除

- 真删除：彻底把属性从对象中移除: delete obj.name

- 假删除：当前属性还存在，只不过属性值为空: obj.name = null






























##### 三、引用数据类型不能作为属性名

```js
let n = {
    x: 100
};
let m = [100, 200];
let obj = {};
obj[n] = "张三"; //=>obj[{x:100}] 但是对象不能作为属性名，需要把其转换为字符串 =>{"[object Object]":"张三" }
obj[m] = "李四"; //=>obj[[100,200]] =>{ "100,200":"李四" }
console.log(obj); 
    
//=>如果非要让属性名是个对象，只能基于ES6中的新数据结构 Map 处理
```

##### 四、数组相对于对象的特点

> 数组是特殊的对象

1、它的属性名是数字，数字从零开始，逐级递增，每一个数字代表着当前项的位置=>我们把这种数字属性名叫做“索引”

2、默认有一个length 属性存储数组的长度

```js
let arr = [10, 20, 30];
console.log(arr[0], arr[1], arr[2]);
console.log(arr.length);
console.log(arr['length']);
```