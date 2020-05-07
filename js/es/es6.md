# ES6

## 第1节：ES6的开发环境搭建

1. 建立工程目录：

    - 先建立一个项目的工程目录，并在目录下边建立两个文件夹：src和dist

        - src：书写ES6代码的文件夹，写的js程序都放在这里。

        - dist：利用Babel编译成的ES5代码的文件夹，在HTML页面需要引入的时这里的js文件。

2. 编写index.html：

    - 文件夹建立好后，我们新建一个index.html文件。

    ```html
    <!DOCTYPE html>
    <html lang="en">
        <head>
            <title></title>
            <meta charset="UTF-8">
            <meta name="viewport" content="width=device-width, initial-scale=1">
            <script src="./dist/index.js"></script>
        </head>
        <body>
            Hello ECMA Script 6
        </body>
    </html>
    ```

3. 编写index.js
    - 在src目录下，新建index.js文件。这个文件很简单，我们只作一个a变量的声明，并用console.log()打印出来。

4. 初始化项目
    - 在安装Babel之前，需要用npm init先初始化我们的项目。打开终端或者通过cmd打开命令行工具，进入项目目录，输入下边的命令：

    ```js
    npm i -y
    ```

4. 全局安装Babel-cli
```js
npm install -g babel-cli
```

5. 本地安装babel-preset-es2015 和 babel-cli

```js
npm install --save-dev babel-preset-es2015 babel-cli
```

6. 新建.babelrc
    - 在根目录下新建.babelrc文件，并打开录入下面的代码
    ```json
    {
        "presets":[
            "es2015"
        ],
        "plugins":[]
    }
    ```
    - 这个文件我们建立完成后，现在可以在终端输入的转换命令了，这次ES6成功转化为ES5的语法。

    ```js
    babel src/index.js -o dist/index.js
    ```

## 第2节：新的声明方式（let和const）

### 1. var声明：

var在ES6里是用来声明全局变量的，我们可以先作一个最简单的实例，用var声明一个变量a,然后用console.log进行输出。

### 2. let局部声明

- 通过两个简单的例子，我们对var的全局声明有了一定了解。那跟var相对应的是let，它是局部变量声明。let是局部变量声明，let声明只在区块内起作用，外部是不可以调用的。
```js
if (true) {
 let a = 40;
 console.log(a); //40
}
console.log(a); // undefined
```
```js
let a = 50;
let b = 100;
if (true) {
 let a = 60;
 var c = 10;
 console.log(a/c); // 6
 console.log(b/c); // 10
}
console.log(c); // 10
console.log(a); // 50
```

### 3. const声明常量

- 用于给变量赋值一个常量。这个值是无法改变，它是固定的。在程序开发中，有些变量是希望声明后在业务层就不再发生变化了，简单来说就是从声明开始，这个变量始终不变，就需要用const进行声明。

```js
const a = 50;
a = 60; // 出错. 你不能改变const的值
const b = "Constant variable";
b = "Assigning new value"; // 出错

const LANGUAGES = ['Js', 'Ruby', 'Python', 'Go'];
LANGUAGES = "Javascript"; // 错误.
LANGUAGES.push('Java'); // 正常.
console.log(LANGUAGES); // ['Js', 'Ruby', 'Python', 'Go', 'Java']
```
- 无论何时定义const变量，Javascript都会将值的内存地址赋值给变量。在我们的示例中，变量'LANGUAGES'实际上指向了分配给数组的内存。因此，你无法在以后更改变量来指向其他内存位置。在整个程序中它只指向数组。

## 第3节：变量的解构赋值

### 1. 数组的解构赋值：
- 简单的数组解构：

- 以前，为变量赋值，我们只能直接指定值。比如下面的代码：

```js
let a=0;
let b=1;
let c=2;
```
- 而现在我们可以用数组解构的方式来进行赋值。

```js
let [a,b,c]=[1,2,3];
```

### 2. 数组模式和赋值模式统一：

- 可以简单的理解为等号左边和等号右边的形式要统一，如果不统一解构将失败。

```js
let [a,[b,c],d]=[1,[2,3],4];
```
- 如果等号两边形式不一样，很可能获得undefined或者直接报错。

### 3. 解构的默认值：

- 解构赋值是允许你使用默认值的，先看一个最简单的默认是的例子。

```js
let [foo = true] =[];
console.log(foo); //控制台打印出true
```
- 需要注意的是undefined和null的区别。

```js
let [a,b="JSPang"]=['技术胖',undefined];
console.log(a+b); //控制台显示“技术胖JSPang”

// undefined相当于什么都没有，b是默认值。
// 右边模式对应的值，必须严格等于undefined，默认值才能生效，而null不严格等于undefined。
let [a,b="JSPang"]=['技术胖',null];
console.log(a+b); //控制台显示“技术胖null”
```
### 4. 对象的解构赋值
- 解构不仅可以用于数组，还可以用于对象。
```js
let {foo,bar} = {foo:'JSPang',bar:'技术胖'};
console.log(foo+bar); //控制台打印出了“JSPang技术胖”
```
- 注意：对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。

- 圆括号的使用：如果在解构之前就定义了变量，这时候你再解构会出现问题。下面是错误的代码，编译会报错。

```js
let foo;
{foo} ={foo:'JSPang'};
console.log(foo);
```
- 要解决报错，使程序正常，我们这时候只要在解构的语句外边加一个圆括号就可以了。

```js
let foo;
({foo} ={foo:'JSPang'});
console.log(foo); //控制台输出jspang
```
### 5. 字符串解构
- 字符串也可以解构，这是因为，此时字符串被转换成了一个类似数组的对象。

```js
const [a,b,c,d,e,f]="JSPang";
console.log(a);
console.log(b);
console.log(c);
console.log(d);
console.log(e);
console.log(f);
```
### 6. 数值和布尔值的解构赋值

解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于<font color=FF0000>undefined</font>和<font color=FF0000>null</font>无法转为对象，所以对它们进行解构赋值，都会报错。
```js
// 数值和布尔值的包装对象都有toString属性
let {toString: s} = 123;
s === Number.prototype.toString // true
let {toString: s} = true;
s === Boolean.prototype.toString // true

let { prop: x } = undefined; // TypeError
let { prop: y } = null;      // TypeError
```


## 第4节：扩展运算符和rest运算符

它们可以很好的为我们解决参数和对象数组未知情况下的编程，让我们的代码更健壮和简洁。

### 1. 对象扩展运算符（…）：简单来说，它将元素列表转换为数组，或者将数组转换成元素列表。

- 当编写一个方法时，我们允许它传入的参数是不确定的。这时候可以使用对象扩展运算符来作参数，看一个简单的列子：

```js
function jspang(...arg){
    console.log(arg[0]);
    console.log(arg[1]);
    console.log(arg[2]);
    console.log(arg[3]);
}
jspang(1,2,3);
// <!--这时我们看到控制台输出了 1,2,3，undefined，这说明是可以传入多个值，并且就算方法中引用多了也不会报错。-->
```

### 2. 扩展运算符的用处：

1. 将元素列表转换为数组

```js
let SumElements = (...arr) => {
console.log(arr); // [10, 20, 40, 60, 90]
let sum = 0;
for (let element of arr) {
sum += element;
}
console.log(sum); // 220. 
}
SumElements(10, 20, 40, 60, 90); // 注意我们这里没有传入数组. 而是将元素作为参数传递。
```

2. 将数组转换为元素列表

```js
let arr = [10, 20, 60];
Math.max(arr); // 出错. 不接受数组.

let arr1 = [10, 20, 60];
Math.max(...arr1); // 60
```

- 我们先用一个例子说明，我们声明两个数组arr1和arr2，然后我们把arr1赋值给arr2，然后我们改变arr2的值，你会发现arr1的值也改变了，因为我们这是对内存堆栈的引用，而不是真正的赋值。

```js
let arr1=['www','jspang','com'];
let arr2=arr1;
console.log(arr2);
arr2.push('shengHongYu');
console.log(arr1);

// <!--控制台输出：-->
["www", "jspang", "com"]
["www", "jspang", "com", "shengHongYu"]
```

- 这是我们不想看到的，可以利用对象扩展运算符简单的解决这个问题，现在我们对代码进行改造。

```js
let arr1=['www','jspang','com'];
//let arr2=arr1;
let arr2=[...arr1];
console.log(arr2);
arr2.push('shengHongYu');
console.log(arr2);
console.log(arr1);

// <!--现在控制台预览时，你可以看到我们的arr1并没有改变，简单的扩展运算符就解决了这个问题。-->
["www", "jspang", "com"]
["www", "jspang", "com", "shengHongYu"]
["www", "jspang", "com"]
```

3. 复制数组：通常我们直接复制数组时，只是浅拷贝，如果要实现深拷贝，可以使用拓展运算符。

```js
// 通常情况 浅拷贝
let a1 = [1, 2];
let a2 = a1; 
a2[0] = 3;
console.log(a1,a2); // [3,2] [3,2]

// 拓展运算符 深拷贝
let a1 = [1, 2];
let a2 = [...a1];
// let [...a2] = a1; // 作用相同
a2[0] = 3;
console.log(a1,a2); // [1,2] [3,2]
```

4. 合并数组：这里合并数组，只是浅拷贝。

```js
let a1 = [1,2];
let a2 = [3];
let a3 = [4,5];

// ES5 
let a4 = a1.concat(a2, a3);

// ES6
let a5 = [...a1, ...a2, ...a3];

a4[0] === a1[0]; // true
a5[0] === a1[0]; // true
```

5. 与解构赋值结合：与解构赋值结合生成数组，但是使用拓展运算符需要放到参数最后一个，否则报错。

```js
let [a, ...b] = [1, 2, 3, 4]; 
// a => 1  b => [2,3,4]

let [a, ...b] = [];
// a => undefined b => []

let [a, ...b] = ["abc"];
// a => "abc"  b => []
```


### 3. rest运算符

如果你已经很好的掌握了对象扩展运算符，那么理解rest运算符并不困难，它们有很多相似之处，甚至很多时候你不用特意去区分。它也用…（三个点）来表示，我们先来看一个例子。

```js
function jspang(first,...arg){
    console.log(arg.length);
}

jspang(0,1,2,3,4,5,6,7);

// <!--这时候控制台打印出了7，说明我们arg里有7个数组元素，这就是rest运算符的最简单用法。-->
```

- rest参数只能放在最后一个，否则报错：

```js
function f(a, ...b, c){...}; // 报错 
```

- 函数的length属性不包含rest参数。

```js
function f1 (a){...};
function f2 (a,...b){...};
f1(1);   // 1
f2(1,2); // 1
```

- 如何循环输出rest运算符

```js
function jspang(first,...arg){
    for(let val of arg){
        console.log(val);
    }
}

jspang(0,1,2,3,4,5,6,7);
```

- for…of的循环可以避免我们开拓内存空间，增加代码运行效率，所以建议大家在以后的工作中使用for…of循环。有的小伙伴会说了，反正最后要转换成ES5，没有什么差别，但是至少从代码量上我们少打了一些单词，这就是开发效率的提高。

## 第5节：(String)字符串的扩展

### 1. 字符串模版

先来看一个在ES5下我们的字符串拼接案例:

```js
let jspang='技术胖';
let blog = '非常高兴你能看到这篇文章，我是你的老朋友'+jspang+'。这节课我们学习字符串模版。';
document.write(blog);
```
ES5下必须用+jspang+这样的形式进行拼接，这样很麻烦而且很容易出错。ES6新增了字符串模版，可以很好的解决这个问题。字符串模版不再使用‘xxx’这样的单引号，而是换成了xxx这种形式，也叫连接号。这时我们再引用jspang变量就需要用${jspang}这种形式了，我们对上边的代码进行改造。

```js
let jspang='技术胖';
let blog = `非常高兴你能看到这篇文章，我是你的老朋友${jspang}。这节课我们学习字符串模版。`;
document.write(blog);
```
- 可以看到浏览器出现了和上边代码一样的结果。而且这里边支持html标签，可以试着输入一些。

```js
let jspang='技术胖';
let blog = `<b>非常高兴你能看到这篇文章</b>，我是你的老朋友${jspang}。<br/>这节课我们学习字符串模版。`;
document.write(blog);
```

### 2. 字符串查找

- ES6还增加了字符串的查找功能，而且支持中文哦，小伙伴是不是很兴奋。还是拿上边的文字作例子，进行操作。

- 查找是否存在:先来看一下ES5的写法，其实这种方法并不实用，给我们的索引位置，我们自己还要确定位置。

```js
let jspang='技术胖';
let blog = '非常高兴你能看到这篇文章，我是你的老朋友技术胖。这节课我们学习字符串模版。';
document.write(blog.indexOf(jspang));
<!--这是网页中输出了20，我们还要自己判断。-->
```

- ES6直接用includes就可以判断，不再返回索引值，返回布尔值，表示是否找到参数字符串。这样的结果我们更喜欢，更直接。

```js
let jspang='技术胖';
let blog = '非常高兴你能看到这篇文章，我是你的老朋友技术胖。这节课我们学习字符串模版。';
document.write(blog.includes(jspang));
```

- 判断开头是否存在：startsWith()返回布尔值，表示参数字符串是否在原字符串的头部。

```js
blog.startsWith(jspang);
```

- 判断结尾是否存在：endsWith()返回布尔值，表示参数字符串是否在原字符串的尾部。

```js
blog.endsWith(jspang);
```

- 并且这三个方法都支持第二个参数，表示起始搜索的位置。

```js
let a = 'hello leo';
a.startsWith('leo',1);   // false
a.endsWith('o',5);       // true
a.includes('lo',6);      // false
```
> endsWith 是针对前 n 个字符，而其他两个是针对从第n个位置直到结束。


### 3. 复制字符串: repeat()返回一个新字符串，表示将原字符串重复n次。

我们有时候是需要字符串重复的，比如分隔符和特殊符号，这时候复制字符串就派上用场了，语法很简单。

基础用法：

```js
document.write('jspang|'.repeat(3));
```

特殊用法:

- 参数为小数，则取整

```js
'ab'.repeat(2.3);      // 'abab'
```

- 参数为负数或Infinity，则报错

```js
'ab'.repeat(-1);       // RangeError
'ab'.repeat(Infinity); // RangeError
```

- 参数为0到-1的小数或NaN，则取0

```js
'ab'.repeat(-0.5);     // ''
'ab'.repeat(NaN);      // ''
```

- 参数为字符串，则转成数字

```js
'ab'.repeat('ab');     // ''
'ab'.repeat('3');      // 'ababab'
```

### 4. 字符串补全：padStart(),padEnd()padStart()为头部补全，padEnd()为尾部补全。

这两个方法接收2个参数
- 第一个指定字符串最小长度

- 第二个用于补全的字符串。

基础用法 ：

```js
'x'.padStart(5, 'ab');   // 'ababx'
'x'.padEnd(5, 'ab');     // 'xabab'
```

特殊用法:

- 原字符串长度，大于或等于指定最小长度，则返回原字符串。

```js
'xyzabc'.padStart(5, 'ab'); // 'xyzabc'
```

- 用来补全的字符串长度和原字符串长度之和，超过指定最小长度，则截去超出部分的补全字符串。
```js
'ab'.padStart(5,'012345'); // "012ab"
```

- 省略第二个参数，则用空格补全。
```js
'x'.padStart(4);           // '    x'
'x'.padEnd(4);           // 'x    '
```

## 第6节：(Number)数字的扩展

### 1. 二进制和八进制

- 二进制声明：二进制的英文单词是Binary,二进制的开始是0（零），然后第二个位置是b（注意这里大小写都可以实现），然后跟上二进制的值就可以了。
    
```js
let binary = 0B010101;
console.log(binary);
<!--这时候浏览器的控制台显示出了21。-->
```
- 八进制声明：八进制的英文单词是Octal，也是以0（零）开始的，然后第二个位置是O（欧），然后跟上八进制的值就可以了。
    
```js
let b=0o666;
console.log(b);
<!--这时候浏览器的控制台显示出了438。-->
```

### 2. 数值的拓展

#### 数字验证Number.isFinite( xx ):

可以使用Number.isFinite( )来进行数字验证，只要是数字，不论是浮点型还是整形都会返回true，其他时候会返回false。

```js
Number.isFinite(10);            // true
Number.isFinite(0.5);           // true
Number.isFinite(NaN);           // false
Number.isFinite(Infinity);      // false
Number.isFinite(-Infinity);     // false
Number.isFinite('leo');         // false
Number.isFinite('15');          // false
Number.isFinite(true);          // false
Number.isFinite(Math.random()); // true
```

#### NaN验证: 

NaN是特殊的非数字，可以使用Number.isNaN()来进行验证。下边的代码控制台返回了true。

```js
Number.isNaN(NaN);      // true
Number.isNaN(10);       // false
Number.isNaN('10');     // false
Number.isNaN(true);     // false
Number.isNaN(5/NaN);    // true
Number.isNaN('true' / 0);      // true
Number.isNaN('true' / 'true'); // true
```
> 区别：与传统全局的isFinite()和isNaN()方法的区别，传统的这两个方法，是先将参数转换成数值，再判断。

```js
isFinite(25);          // true
isFinite("25");        // true
Number.isFinite(25);   // true
Number.isFinite("25"); // false

isNaN(NaN);            // true
isNaN("NaN");          // true
Number.isNaN(NaN);     // true
Number.isNaN("NaN");   // false
```

#### 判断是否为整数Number.isInteger(xx)

```js
Number.isInteger(10);   // true
Number.isInteger(10.0); // true
Number.isInteger(10.1); // false
```

#### 整数转换Number.parseInt(xxx)和浮点型转换Number.parseFloat(xxx)

```js
let a='9.18';
console.log(Number.parseInt(a)); 
console.log(Number.parseFloat(a));
```

#### Math对象的拓展

ES6新增17个数学相关的静态方法，只能在Math对象上调用。

##### 1. Math.trunc:
    
    - 用来去除小数的小数部分，返回整数部分。
    
    - 若参数为非数值，则先转为数值。
    
    - 若参数为空值或无法截取整数的值，则返回NaN。
```js
// 正常使用
Math.trunc(1.1);     // 1
Math.trunc(1.9);     // 1
Math.trunc(-1.1);    // -1
Math.trunc(-1.9);    // -1
Math.trunc(-0.1234); // -0

// 参数为非数值
Math.trunc('11.22'); // 11
Math.trunc(true);    // 1
Math.trunc(false);   // 0
Math.trunc(null);    // 0

// 参数为空和无法取整
Math.trunc(NaN);       // NaN
Math.trunc('leo');     // NaN
Math.trunc();          // NaN
Math.trunc(undefined); // NaN

// ES5实现
Math.trunc = Math.trunc || function(x){
    return x < 0 ? Math.ceil(x) : Math.floor(x);
}
```

##### 2. Math.sign(): 判断一个数是正数、负数还是零，对于非数值，会先转成数值。返回值：
    
    - 参数为正数， 返回 +1
    
    - 参数为负数， 返回 -1
    
    - 参数为0， 返回 0
    
    - 参数为-0， 返回 -0
    
    - 参数为其他值， 返回 NaN
```js
Math.sign(-1);   // -1
Math.sign(1);    // +1
Math.sign(0);    // 0
Math.sign(-0);   // -0
Math.sign(NaN);  // NaN

Math.sign('');   // 0
Math.sign(true); // +1
Math.sign(false);// 0
Math.sign(null); // 0
Math.sign('9');  // +1
Math.sign('leo');// NaN
Math.sign();     // NaN
Math.sign(undefined); // NaN

// ES5实现
Math.sign = Math.sign || function (x){
    x = +x;
    if (x === 0 || isNaN(x)){
        return x;
    }
    return x > 0 ? 1: -1;
}
```

##### 3. Math.cbrt(): 用来计算一个数的立方根，若参数为非数值则先转成数值。

```js
Math.cbrt(-1); // -1
Math.cbrt(0);  // 0
Math.cbrt(1);  // 1
Math.cbrt(2);  // 1.2599210498

Math.cbrt('1');   // 1
Math.cbrt('leo'); // NaN

// ES5实现
Math.cbrt = Math.cbrt || function (x){
    var a = Math.pow(Math.abs(x), 1/3);
    return x < 0 ? -y : y;
}
```
##### 3. Math.clz32(): 用于返回一个数的 32 位无符号整数形式有多少个前导 0。
```js
Math.clz32(0) // 32
Math.clz32(1) // 31
Math.clz32(1000) // 22
Math.clz32(0b01000000000000000000000000000000) // 1
Math.clz32(0b00100000000000000000000000000000) // 2
```

##### 4. Math.imul(): 用于返回两个数以 32 位带符号整数形式相乘的结果，返回的也是一个 32 位的带符号整数。

```js
Math.imul(2, 4)   // 8
Math.imul(-1, 8)  // -8
Math.imul(-2, -2) // 4
```

##### 5. Math.fround(): 用来返回一个数的**2位单精度浮点数**形式。

```js
Math.fround(0)   // 0
Math.fround(1)   // 1
Math.fround(2 ** 24 - 1)   // 16777215
```

##### 6. Math.hypot(): 用来返回所有参数的平方和的**平方根**。

```js
Math.hypot(3, 4);        // 5
Math.hypot(3, 4, 5);     // 7.0710678118654755
Math.hypot();            // 0
Math.hypot(NaN);         // NaN
Math.hypot(3, 4, 'foo'); // NaN
Math.hypot(3, 4, '5');   // 7.0710678118654755
Math.hypot(-3);          // 3
```

##### 7. Math.expm1(): 用来返回ex - 1，即Math.exp(x) - 1。

```js
Math.expm1(-1) // -0.6321205588285577
Math.expm1(0)  // 0
Math.expm1(1)  // 1.718281828459045

// ES5实现
Math.expm1 = Math.expm1 || function(x) {
  return Math.exp(x) - 1;
};
```

##### 8. Math.log1p(): 用来返回1 + x的自然对数，即Math.log(1 + x)。如果x小于-1，返回NaN。

```js
Math.log1p(1)  // 0.6931471805599453
Math.log1p(0)  // 0
Math.log1p(-1) // -Infinity
Math.log1p(-2) // NaN

// ES5实现
Math.log1p = Math.log1p || function(x) {
  return Math.log(1 + x);
};
```

##### 9. Math.log10(): 用来返回以 10为底的x的对数。如果x小于 0，则返回 NaN。

```js
Math.log10(2)      // 0.3010299956639812
Math.log10(1)      // 0
Math.log10(0)      // -Infinity
Math.log10(-2)     // NaN
Math.log10(100000) // 5

// ES5实现
Math.log10 = Math.log10 || function(x) {
  return Math.log(x) / Math.LN10;
};
```

##### 10. Math.log2(): 用来返回以 2 为底的x的对数。如果x小于0，则返回 NaN。

```js
Math.log2(3)       // 1.584962500721156
Math.log2(2)       // 1
Math.log2(1)       // 0
Math.log2(0)       // -Infinity
Math.log2(-2)      // NaN
Math.log2(1024)    // 10
Math.log2(1 << 29) // 29

// ES5实现
Math.log2 = Math.log2 || function(x) {
  return Math.log(x) / Math.LN2;
};
```

##### 11. 双曲函数方法:

- Math.sinh(x) 返回x的双曲正弦（hyperbolic sine）

- Math.cosh(x) 返回x的双曲余弦（hyperbolic cosine）

- Math.tanh(x) 返回x的双曲正切（hyperbolic tangent）

- Math.asinh(x) 返回x的反双曲正弦（inverse hyperbolic sine）

- Math.acosh(x) 返回x的反双曲余弦（inverse hyperbolic cosine）

- Math.atanh(x) 返回x的反双曲正切（inverse hyperbolic tangent）

##### 12. 指数操作: 新增的指数运算符(**)和Math.pow()
```js
2 ** 2; // 4
2 ** 3; // 8 

2 ** 3 ** 2; // 相当于 2 ** (3 ** 2); 返回 512
```

- 整数的操作是有一个取值范围的，它的取值范围就是2的53次方。我们先用程序来看一下这个数字是什么.
    ```js
    let a = Math.pow(2,53)-1;
    console.log(a); //9007199254740991
    ```
- 最大安全整数:在我们计算时会经常超出这个值，所以我们要进行判断，ES6提供了一个常数，叫做最大安全整数，以后就不需要我们计算了。
    ```js
    console.log(Number.MAX_SAFE_INTEGER);
    ```
- 最小安全整数
    ```js
    console.log(Number.MIN_SAFE_INTEGER);
    ```
- 安全整数判断isSafeInteger( )
    ```js
    let a= Math.pow(2,53)-1;
    console.log(Number.isSafeInteger(a));//false
    ```
> 指数运算符(**)与Math.pow的实现不相同，对于特别大的运算结果，两者会有细微的差异。

```js
Math.pow(99, 99)
// 3.697296376497263e+197

99 ** 99
// 3.697296376497268e+197
```

## 第7节：(Array)数组的扩展

### 1. JSON数组格式转换

JSON的数组格式就是为了前端快速的把JSON转换成数组的一种格式，我们先来看一下JSON的数组格式怎么写。

```js
let  json = {
    '0': 'jspang',
    '1': '技术胖',
    '2': '大胖逼逼叨',
    length:3
}
```
这就是一个标准的JSON数组格式，跟普通的JSON对比是在最后多了一个length属性。只要是这种特殊的json格式都可以轻松使用ES6的语法转变成数组。在ES6中绝大部分的Array操作都存在于Array对象里。我们就用Array.from(xxx)来进行转换。我们把上边的JSON代码转换成数组，并打印在控制台。

```js
let  json = {
    '0': 'jspang',
    '1': '技术胖',
    '2': '大胖逼逼叨',
    length:3
}
    
let arr=Array.from(json);
console.log(arr)
```

### 2. Array.of()方法：

它负责把一堆文本或者变量转换成数组。在开发中我们经常拿到了一个类似数组的字符串，需要使用eval来进行转换，如果你一个老手程序员都知道eval的效率是很低的，它会拖慢我们的程序。这时候我们就可以使用Array.of方法。我们看下边的代码把一堆数字转换成数组并打印在控制台上：
    
```js
let arr =Array.of(3,4,5,6);
console.log(arr);
Array.of(1,2,3);    // [1,2,3]
Array.of(1).length; // 1

Array();       // []
Array(2);      // [,] 1个参数时，为指定数组长度
Array(1,2,3);  // [1,2,3] 多于2个参数，组成新数组
```
当然它不仅可以转换数字，字符串也是可以转换的，看下边的代码：

```js
let arr =Array.of('技术胖','jspang','大胖逼逼叨');
console.log(arr);
```

### 3. find()和findIndex()实例方法:

> <font color=FF0000>find()</font>方法用于找出第一个符合条件的数组成员，参数为一个回调函数，所有成员依次执行该回调函数，返回第一个返回值为<font color=FF0000>true</font>的成员，如果没有一个符合则返回<font color=FF0000>undefined</font>。

所谓的实例方法就是并不是以Array对象开始的，而是必须有一个已经存在的数组，然后使用的方法，这就是实例方法（不理解请看下边的代码，再和上边的代码进行比对，你会有所顿悟）。这里的find方法是从数组中查找。在find方法中我们需要传入一个匿名函数，函数需要传入三个参数：

1. value：表示当前查找的值。

2. index：表示当前查找的数组索引。

3. arr：表示当前数组。

在函数中如果找到符合条件的数组元素就进行return，并停止查找。你可以拷贝下边的代码进行测试，就会知道find作用。

```js
let arr=[1,2,3,4,5,6,7,8,9];
console.log(arr.find(function(value,index,arr){
    return value > 5;
}))
//控制台输出了6，说明找到了符合条件的值，并进行返回了，如果找不到会显示undefined。
```

> <font color=FF0000>findIndex()</font>方法与<font color=FF0000>find()</font>类似，返回第一个符合条件的数组成员的位置，如果都不符合则返回<font color=FF0000>-1</font>。

```js
[1,2,3,4].findIndex((v,i,a)=>{
    return v>2;
}); // 2
```

### 4. fill( )实例方法：

fill()也是一个实例方法，它的作用是把数组进行填充，它接收三个参数，

- 第一个参数是填充的变量，

- 第二个是开始填充的位置，

- 第三个是填充到的位置。

```js
let arr=[0,1,2,3,4,5,6,7,8,9];
arr.fill('jspang',2,5);
console.log(arr);
<!--上边的代码是把数组从第二位到第五位用jspang进行填充。-->
new Array(3).fill('a');   // ['a','a','a']
[1,2,3].fill('a');        // ['a','a','a']
```

### 5. 数组的遍历: for..of遍历元素列表（即），如Array，并逐个返回元素（不是它们的索引）

- for…of循环：这种形式比ES5的for循环要简单而且高效。先来看一个最简单的for…of循环。
    
    ```js
    let arr=['jspang','技术胖','大胖逼逼叨']
        
    for (let item of arr){
        console.log(item);
    }
    ```
- for…of数组索引:有时候开发中是需要数组的索引的，那我们可以使用下面的代码输出数组索引。
    
    ```js
    let arr=['jspang','技术胖','大胖逼逼叨']
    for (let index of arr.keys()){
        console.log(index);
    }
    // <!--可以看到这时的控制台就输出了0,1,2，也就是数组的索引。-->
    ```
- 同时输出数组的内容和索引：我们用entries()这个实例方法，配合我们的for…of循环就可以同时输出内容和索引了。

    ```js
    let arr=['jspang','技术胖','大胖逼逼叨']
    for (let [index,val] of arr.entries()){
        console.log(index+':'+val);
    }
    ```
- 同时for...of循环也适用于字符串
    ```js
    let string = "Javascript";
    for (let char of string) {
    console.log(char);
    }
    Output:
    J
    a
    v
    a
    s
    c
    r
    i
    p
    t
    ```

### 6. entries(),keys(),values()

> 主要用于遍历数组，<font color=FF0000>entries()</font>对键值对遍历，<font color=FF0000>keys()</font>对键名遍历，<font color=FF0000>values()</font>对键值遍历。

```js
for (let i of ['a', 'b'].keys()){
    console.log(i)
}
// 0
// 1

for (let e of ['a', 'b'].values()){
    console.log(e)
}
// 'a'
// 'b'

for (let e of ['a', 'b'].entries()){
    console.log(e)
}
// [0, "a"] 
// [1, "b"]
```

entries()实例方式生成的是Iterator形式的数组，那这种形式的好处就是可以让我们在需要时用next()手动跳转到下一个值。我们来看下面的代码：
    
```js
let arr=['jspang','技术胖','大胖逼逼叨']
let list=arr.entries();
console.log(list.next().value);
console.log(list.next().value);
console.log(list.next().value);
```

### 7. Array.from(): 

将**类数组对象** 和 **可遍历的对象**，转换成真正的数组。

```js
// 类数组对象
let a = {
    '0':'a',
    '1':'b',
    length:2
}
let arr = Array.from(a);

// 可遍历的对象
let a = Array.from([1,2,3]);
let b = Array.from({length: 3});
let c = Array.from([1,2,3]).map(x => x * x);
let d = Array.from([1,2,3].map(x => x * x));
```

### 8. includes():

用于表示数组是否包含给定的值，与字符串的includes方法类似。

```js
[1,2,3].includes(2);     // true
[1,2,3].includes(4);     // false
[1,2,NaN].includes(NaN); // true
```

第二个参数为起始位置，默认为0，如果负数，则表示倒数的位置，如果大于数组长度，则重置为0开始。

```js
[1,2,3].includes(3,3);    // false
[1,2,3].includes(3,4);    // false
[1,2,3].includes(3,-1);   // true
[1,2,3].includes(3,-4);   // true
```

### 9. flat()和flatMap()：

<font color=FF0000>flat()</font>用于将数组一维化，返回一个新数组，不影响原数组。默认一次只一维化一层数组，若需多层，则传入一个整数参数指定层数。若要一维化所有层的数组，则传入Infinity作为参数。

```js
[1, 2, [2,3]].flat();        // [1,2,2,3]
[1,2,[3,[4,[5,6]]]].flat(3); // [1,2,3,4,5,6]
[1,2,[3,[4,[5,6]]]].flat('Infinity'); // [1,2,3,4,5,6]
```

<font color=FF0000>flatMap()</font>是将原数组每个对象先执行一个函数，在对返回值组成的数组执行flat()方法，返回一个新数组，不改变原数组。

- flatMap()只能展开一层。

```js
[2, 3, 4].flatMap((x) => [x, x * 2]); 
// [2, 4, 3, 6, 4, 8] 
```



## 第9节：(Function)函数的扩展

### 1. 默认参数: 默认参数是在声明函数时默认给出的参数。

在ES6中给我们增加了默认参数的操作，我们修改上边的代码，可以看到现在只需要传递一个参数也是可以正常运行的。

```js
function add(a,b=1){
    return a+b;
}
console.log(add(1));
```

> 参数变量是默认声明的，不能用let和const再次声明：
```js
function f (a = 1){
    let a = 2; // error
}
```

主动抛出错误

- 在使用Vue的框架中，可以经常看到框架主动抛出一些错误，比如v-for必须有:key值。那尤大神是如何做到的那？其实很简单，ES6中我们直接用throw new Error( xxxx ),就可以抛出错误。

```js
function add(a,b=1){
    
    if(a == 0){
        throw new Error('This is error')
    }
        return a+b;
}
    
console.log(add(0));
```

尾参数定义默认值:

- 通常在尾参数定义默认值，便于观察参数，并且非尾参数无法省略。

```js
function f (a=1,b){
    return [a, b];
}
f();    // [1, undefined]
f(2);   // [2, undefined]
f(,2);  // 报错

f(undefined, 2);  // [1, 2]

function f (a, b=1, c){
    return [a, b, c];
}
f();        // [undefined, 1, undefined]
f(1);       // [1,1,undefined]
f(1, ,2);   // 报错
f(1,undefined,2); // [1,1,2]
```

> 在给参数传递默认值时，传入undefined会触发默认值，传入null不会触发。

```js
function f (a = 1, b = 2){
    console.log(a, b);
}
f(undefined, null); // 1 null
```

### 2. 函数的length属性:

length属性将返回，没有指定默认值的参数数量，并且rest参数不计入length属性。

```js
function f1 (a){...};
function f2 (a=1){...};
function f3 (a, b=2){...};
function f4 (...a){...};
function f5 (a,b,...c){...};

f1.length; // 1
f2.length; // 0
f3.length; // 1
f4.length; // 0
f5.length; // 2
```
如果你在使用别人的框架时，不知道别人的函数需要传递几个参数怎么办？ES6为我们提供了得到参数的方法(xxx.length).我们用上边的代码看一下需要传递的参数个数。

```js
function add(a,b){
    'use strict'
    if(a == 0){
        throw new Error('This is error');
    }
        return a+b;
}
    
console.log(add.length);
```
- 这时控制台打印出了2，但是如果我们去掉严谨模式，并给第二个参数加上默认值的话，这时候add.length的值就变成了1， 也就是说它得到的是必须传入的参数。

### 3. 函数中的严谨模式

我们在ES中就经常使用严谨模式来进行编程，但是必须写在代码最上边，相当于全局使用。在ES6中我们可以写在函数体中，相当于针对函数来使用。

```js
function add(a,b=1){
    'use strict'
    if(a == 0){
        throw new Error('This is error');
    }
        return a+b;
}
    
console.log(add(1));
```

上边的代码如果运行的话，你会发现浏览器控制台报错，这是ES6中的一个坑，如果没人指导的话，可能你会陷进去一会。这个错误的原因就是如果你使用了默认值，再使用严谨模式的话，就会有冲突，所以我们要取消默认值的操作，这时候你在运行就正常了。

```js
function add(a,b){
    'use strict'
    if(a == 0){
        throw new Error('This is error');
    }
        return a+b;
}
    
console.log(add(1,2));
```

### 4. 箭头函数

```js
// 老语法
function oldOne() {
 console.log("Hello World..!");
}
// 新语法
var newOne = () => {
 console.log("Hello World..!");
}
// 第一部分是声明一个变量并为其分配函数（即）（）。它只是说变量实际上是一个函数。
// 第二部分声明函数体。 带有花括号的箭头部分定义了函数体。
```

在学习Vue的时候，我已经大量的使用了箭头函数，因为箭头函数真的很好用，我们来看一个最简单的箭头函数。也就是上边我们写的add函数，进行一个改变，写成箭头函数。

```js
var add =(a,b=1) => a+b;
console.log(add(1));
```
{}的使用

- 在箭头函数中，方法体内如果是两句话，那就需要在方法体外边加上{}括号。例如下边的代码就必须使用{}.

```js
var add =(a,b=1) => {
    console.log('jspang')
    return a+b;
};
console.log(add(1));
```

> 注意点：

1. 箭头函数内的this总是指向定义时所在的对象，而不是调用时。

2. 箭头函数不能当做构造函数，即不能用new命令，否则报错。

3. 箭头函数不存在arguments对象，即不能使用，可以使用rest参数代替。

4. 箭头函数不能使用yield命令，即不能用作Generator函数。

### 5. name 属性

用于返回该函数的函数名。

```js
function f (){...};
f.name;    // f

const f = function g(){...};
f.name;    // g
```

## 第10节：ES6中的函数和数组补漏

### 1. 对象的函数解构

我们在前后端分离时，后端经常返回来JSON格式的数据，前端的美好愿望是直接把这个JSON格式数据当作参数，传递到函数内部进行处理。ES6就为我们提供了这样的解构赋值。

```js
let json = {
    a:'jspang',
    b:'技术胖'
}
function fun({a,b='jspang'}){
    console.log(a,b);
}
fun(json)
```

### 2. 数组的函数解构

函数能解构JSON，那解构我们的数组就更不在话下了，我们看下边的代码。我们声明一个数组，然后写一个方法，最后用…进行解构赋值。

```js
let arr = ['jspang','技术胖','免费教程'];
function fun(a,b,c){
    console.log(a,b,c);
}
    
fun(...arr);
```
### 3. in的用法

in是用来判断对象或者数组中是否存在某个值的。我们先来看一下用in如何判断对象里是否有某个值。
    
1. 对象判断

    ```js
    let obj={
        a:'jspang',
        b:'技术胖'
    }
    console.log('a' in obj);  //true
    ```

2. 数组判断
    - 先来看一下ES5判断的弊端，以前会使用length属性进行判断，为0表示没有数组元素。但是这并不准确，或者说真实开发中有弊端。

    ```js
    let arr=[,,,,,];
    console.log(arr.length); //5
    ```
    - 上边的代码输出了5，但是数组中其实全是空值，这就是一个坑啊。那用ES6的in就可以解决这个问题。

    ```js
    let arr=[,,,,,];
    console.log(0 in arr); //false
        
    let arr1=['jspang','技术胖'];
    console.log(0 in arr1);  // true
    
    <!--注意：这里的0指的是数组下标位置是否为空。-->
    ```

### 4. 数组的遍历方法

1. forEach

    ```
    let arr=['jspang','技术胖','前端教程'];
        
    arr.forEach((val,index)=>console.log(index,val));
    ```
    
    - forEach循环的特点是会自动省略为空的数组元素，相当于直接给我们筛空了。当是有时候也会给我们帮倒忙。

2. filter（数组过滤）: 数组过滤器用于根据某些条件过滤整个数组。数组过滤器获取数组的每个元素并检查给定条件。如果元素通过条件，它将元素保留在数组中，否则它将删除元素。
    - 参数：(元素本身, 元素的索引, 整个数组)
    ```js
    let arr = [1,2,3,4,5,6] 
    let modifiedArr = arr.filter（function（element，index，array）{ 
    return element％2 == 0 
    }）; 
    console.log（modifiedArr）;
    输出：
    [2,4,6]
    ```
    - 我们必须为数组的每个元素返回一个布尔值。如果您不在末尾返回任何布尔值，则filter将其视为false并删除该元素。
    - 这种方法在Vue实战里我讲过，他其实也有循环的功能，这里我们在复习一遍。

3. some

    ```
    let arr=['jspang','技术胖','前端教程'];
        
    arr.some(x=>console.log(x));
    ```

4. map（数组映射）: Map运算符用于对数组的所有元素执行特定操作，并返回包含已修改元素的数组。

    - 参数: (元素本身, 元素的索引, 整个数组), 第二个和第三个参数只是可选的。只有第一个参数是必需的。
    ```js
    let arr=['jspang','技术胖','前端教程'];
        
    console.log(arr.map(x=>'web')); // [ "web", "web", "web" ]
    // <!--map在这里起到一个替换的作用-->

    let arr = [1,2,3,4,5];
    let modifiedArr = arr.map（function（element，index，arr）{ 
    return element * 10; 
    }）; 
    console.log（modifiedArr）;
    输出：
    [10,20,30,40,50]
    // 注意我们最终必须返回一些值。这将是该元素的修改值。如果您没有返回任何内容，那么特定元素将是未定义的。
    eg: 
    console.log(arr.map(x=>{})); //  [ undefined, undefined, undefined ]
    ```
5. reduce: reduce(数组降维)用于聚合数组的所有元素并返回单个值。
    
    - 与filter和map不同，reduce使用具有四个参数的函数以及一个附加元素。在我们的例子中，它是0。
    
    - 第一个参数是聚合器元素。它是所有元素总和，并且可以给定一个初始值。它的初始值被定义为附加元素。

    ```js
    let arr = [1,2,3,4,5,6] 
    let total = arr.reduce（function（sum，element，index，array）{ 
    return sum + element; 
    }，0）; 
    console.log（“total is”+ total）;
    输出：
    total is 21
    ```
    - 将聚合器元素总和的初始值设置为10。
    ```js
    let arr = [1,2,3,4,5,6]; 
    let totalSum = arr.reduce（function（sum，element，index，array）{ 
    console.log（sum +“+”+ element +“=”+ sum + element）; 
    return sum + element; 
    }，10）; 
    console.log（“Total sum is ”+ totalSum）;
    输出：
    10 + 1 = 11 
    11 + 2 = 13 
    13 + 3 = 16 
    16 + 4 = 20 
    20 + 5 = 25 
    25 + 6 = 31 
    Total sum is 31
        ```
### 5. 数组转换字符串

- 在开发中我们经常会碰到把数组输出成字符串的形式，我们今天学两种方法，你要注意两种方法的区别。
    
    1. join()方法

    ```
    let arr=['jspang','技术胖','前端教程'];
     
    console.log(arr.join('|'));
    <!--join()方法就是在数组元素中间，加了一些间隔，开发中很有用处。-->
    ```
    2. toString()方法

        ```
        let arr=['jspang','技术胖','前端教程'];
         
        console.log(arr.toString());
        
        <!--转换时只是是用逗号隔开了。-->
        ```
    
## 第11节：(Object)对象的扩展

### 1. 对象赋值

ES6允许把声明的变量直接赋值给对象，我们看下面的例子。

```js
let name="jspang";
let skill= 'web';
var obj= {name,skill};
console.log(obj);  //Object {name: "jspang", skill: "web"}
```

### 2. 对象Key值构建

有时候我们会在后台取出key值，而不是我们前台定义好的，这时候我们如何构建我们的key值那。比如我们在后台取了一个key值，然后可以用[ ] 的形式，进行对象的构建。

```js
let key='skill';
var obj={
    [key]:'web'
}
console.log(obj.skill);
```

### 3. Object.is(  ) 对象比较

- Object.is() 用于比较两个值是否严格相等，在ES5时候只要使用相等运算符(==)和严格相等运算符(===)就可以做比较，但是它们都有缺点，前者会自动转换数据类型，后者的NaN不等于自身，以及+0等于-0。
```js
Object.is('a','a');   // true
Object.is({}, {});    // false

// ES5
+0 === -0 ;           // true
NaN === NaN;          // false

// ES6
Object.is(+0,-0);     // false
Object.is(NaN,NaN);   // true
```

对象的比较方法,以前进行对象值的比较，经常使用===来判断，比如下面的代码：

```js
var obj1 = {name:'jspang'};
var obj2 = {name:'jspang'};
console.log(obj1.name === obj2.name);//true
```

那ES6为我们提供了is方法进行对比。

```js
var obj1 = {name:'jspang'};
var obj2 = {name:'jspang'};
console.log(obj1.name === obj2.name);//true
console.log(Object.is(obj1.name,obj2.name)); //true
```

区分=== 和 is方法的区别是什么，看下面的代码输出结果。

```js
console.log(+0 === -0);  //true
console.log(NaN === NaN ); //false
console.log(Object.is(+0,-0)); //false
console.log(Object.is(NaN,NaN)); //true
```

- 这太诡异了，我要怎么记忆，那技术胖在这里告诉你一个小妙招，===为同值相等，is()为严格相等。

### 4. Object.assign(  )合并对象

- Object.assign()方法用于对象的合并，将原对象的所有可枚举属性复制到目标对象。

操作数组时我们经常使用数组合并，那对象也有合并方法，那就是assgin(  )。看一下啊具体的用法。

```js
// 第一个参数是目标对象，后面参数都是源对象。

var a={a:'jspang'};
var b={b:'技术胖'};
var c={c:'web'};
    
let d=Object.assign(a,b,c)
console.log(d);
```

注意：

- 若目标对象与源对象有同名属性，则后面属性会覆盖前面属性。
```js
let a = {a:1, b:2};
let b = {b:3, c:4};
Object.assign(a, b); // a => {a:1, b:3, c:4}
```

- 若只有一个参数，则返回该参数。
```js
let a = {a:1};
Object.assign(a) === a;  // true
```

- 若参数不是对象，则先转成对象后返回。
```js
typeof Object.assign(2); // 'object'
```

- 由于undefined或NaN无法转成对象，所以做为参数会报错。
```js
Object.assign(undefined) // 报错
Object.assign(NaN);      // 报错
```

- 将数组当做对象处理，键名为数组下标，键值为数组下标对应的值。

```js
Object.assign([1, 2, 3], [4, 5]); // [4, 5, 3]
```

> Object.assign()实现的是浅拷贝: Object.assign()拷贝得到的是这个对象的引用。这个对象的任何变化，都会反映到目标对象上面。

```js
let a = {a: {b:1}};
let b = Object.assign({},a);
a.a.b = 2;
console.log(b.a.b);  // 2
```

## 第12节：Symbol

ES6引入Symbol作为一种新的原始数据类型，表示独一无二的值，主要是为了防止属性名冲突。

ES6之后，JavaScript一共有其中数据类型：<font color=FF0000>Symbol、undefined、null、Boolean、String、Number、Object</font>。

```js
let a = Symbol();
typeof a; // "symbol"
```

### 1. 声明Symbol

我们先来回顾一下我们的数据类型，在最后在看看Symbol如何声明，并进行一个数据类型的判断。

<font color=FF0000>Symbol</font>函数不能用<font color=FF0000>new</font>，会报错。由于<font color=FF0000>Symbol</font>是一个原始类型，不是对象，所以不能添加属性，它是类似于字符串的数据类型。

Symbol都是不相等的，即使参数相同。

```js
var a = new String;
var b = new Number;
var c = new Boolean;
var d = new Array;
var e = new Object; 
var f= Symbol();
console.log(typeof(d));

// 没有参数
let a1 = Symbol();
let a2 = Symbol();
a1 === a2; // false 

// 有参数
let a1 = Symbol('abc');
let a2 = Symbol('abc');
a1 === a2; // false 
```

### 2. Symbol的介绍

Symbol可以显式转换为字符串：我们先声明一个Symbol，然后我们在控制台输出一下。

```js
var g = Symbol('jspang');
console.log(g);
console.log(g.toString());
```

Symbol不能与其他类型的值计算，会报错。

```js
let a = Symbol('hello');
a + " world!";  // 报错
`${a} world!`;  // 报错
```
Symbol可以转换为布尔值，但不能转为数值：

```js
let a1 = Symbol();
Boolean(a1);
!a1;        // false

Number(a1); // TypeError
a1 + 1 ;    // TypeError
```

- 这时候我们仔细看控制台是有区别的，没有toString的是红字，toString的是黑字。

### 3. Symbol在对象中的应用

看一下如何用Symbol构建对象的Key，并调用和赋值。

```js
var jspang = Symbol();
var obj={
    [jspang]:'技术胖'
}
console.log(obj[jspang]);
obj[jspang]='web';
console.log(obj[jspang]);
```

好处：防止同名属性，还有防止键被改写或覆盖。

```js
let a1 = Symbol();

// 写法1
let b = {};
b[a1] = 'hello';

// 写法2
let b = {
    [a1] : 'hello'
} 

// 写法3
let b = {};
Object.defineProperty(b, a1, {value : 'hello' });

// 3种写法 结果相同
b[a1]; // 'hello'
```

> 需要注意： Symbol作为对象属性名时，不能用点运算符，并且必须放在方括号内。

```js
let a = Symbol();
let b = {};

// 不能用点运算
b.a = 'hello';
b[a] ; // undefined
b['a'] ; // 'hello'

// 必须放在方括号内
let c = {
    [a] : function (text){
        console.log(text);
    }
}
c[a]('leo'); // 'leo'

// 上面等价于 更简洁
let c = {
    [a](text){
        console.log(text);
    }
}
```

### 4. Symbol对象元素的保护作用

Symbol作为属性名遍历，不出现在<font color=FF0000>for...in、for...of</font>循环，也不被<font color=FF0000>Object.keys()、Object.getOwnPropertyNames()、JSON.stringify()</font>返回。

```js
let a = Symbol('aa'),b= Symbol('bb');
let obj = {
    [a]:'11', [b]:'22'
}
for(let k of Object.values(obj)){console.log(k)}
// 无输出

let obj = {};
let aa = Symbol('leo');
Object.defineProperty(obj, aa, {value: 'hi'});

for(let k in obj){
    console.log(k); // 无输出
}

Object.getOwnPropertyNames(obj);   // []
Object.getOwnPropertySymbols(obj); // [Symbol(leo)]
```

Object.getOwnPropertySymbols方法返回一个数组，包含当前对象所有用做属性名的Symbol值。

```js
let a = {};
let a1 = Symbol('a');
let a2 = Symbol('b');
a[a1] = 'hi';
a[a2] = 'oi';

let obj = Object.getOwnPropertySymbols(a);
obj; //  [Symbol(a), Symbol(b)]
```

另外可以使用Reflect.ownKeys方法可以返回所有类型的键名，包括常规键名和 Symbol 键名。

```js
let a = {
    [Symbol('leo')]: 1,
    aa : 2, 
    bb : 3,
}
Reflect.ownKeys(a); // ['aa', 'bb',Symbol('leo')]
```


在对象中有很多值，但是循环输出时，并不希望全部输出，那我们就可以使用Symbol进行保护。

- 没有进行保护的写法：
    
```js
var obj={name:'jspang',skill:'web',age:18};
    
for (let item in obj){
    console.log(obj[item]);
}
```
- 现在我不想别人知道我的年龄，这时候我就可以使用Symbol来进行循环保护。

```js
let obj={name:'jspang',skill:'web'};
let age=Symbol();
obj[age]=18;
for (let item in obj){
    console.log(obj[item]);
} 
console.log(obj);
```

### 5. Symbol.for()、Symbol.keyFor()

- Symbol.for()

用于**重复使用一个Symbol值**，接收一个**字符串**作为参数，若存在用此参数作为名称的Symbol值，返回这个Symbol，否则新建并返回以这个参数为名称的Symbol值。

```js
let a = Symbol.for('aaa');
let b = Symbol.for('aaa');

a === b;  // true
```

<font color=FF0000>Symbol()</font> 和 <font color=FF0000>Symbol.for()</font>区别：

```js
Symbol.for('aa') === Symbol.for('aa'); // true
Symbol('aa') === Symbol('aa');         // false
```

- Symbol.keyFor()

**用于返回一个已使用的Symbol类型的key**:

```js
let a = Symbol.for('aa');
Symbol.keyFor(a);   //  'aa'

let b = Symbol('aa');
Symbol.keyFor(b);   //  undefined
```

## 第13节：Set和WeakSet数据结构

**Set**数据结构类似数组，但所有成员的值唯一。

### 1. Set的声明: 用来保存任何类型的唯一值

```js
var sets = new Set();
sets.add('a');
sets.add('b');
sets.add('a'); // 添加重复的值.
for (let element of sets) {
 console.log(element);
}
输出:
a
b
let setArr = new Set(['jspang','技术胖','web','jspang']);
console.log(setArr);//Set {"jspang", "技术胖", "web"}
```
- Set和Array 的区别是Set不允许内部有重复的值，如果有只显示一个，相当于去重。虽然Set很像数组，但是他不是数组。

- Set是可迭代的对象。 我们必须遍历元素才能显示它。

### 2. Set属性值和增删查方法

- size: 返回set的大小

- 追加add：在使用Array的时候，可以用push进行追加值，那Set稍有不同，它用更语义化的add进行追加。

添加某个值，返回 Set 结构本身。

```js
let setArr = new Set(['jspang','技术胖','web','jspang']);
console.log(setArr);//Set {"jspang", "技术胖", "web"}
    
setArr.add('前端职场');
console.log(setArr);
```

> 向Set中添加值的时候，不会类型转换，即5和'5'是不同的。

```js
[...new Set([5,'5'])]; // [5, "5"]
```

- 删除delete：删除某个值，返回一个布尔值，表示删除是否成功。

```js
let setArr = new Set(['jspang','技术胖','web','jspang']);
console.log(setArr);//Set {"jspang", "技术胖", "web"}
    
setArr.add('前端职场');
console.log(setArr); //Set {"jspang", "技术胖", "web", "前端职场"}
    
setArr.delete('前端职场');
console.log(setArr); //Set {"jspang", "技术胖", "web"}
```

- 查找has：返回一个布尔值，表示该值是否为Set的成员。

```js
let setArr = new Set(['jspang','技术胖','web','jspang']);
console.log(setArr);//Set {"jspang", "技术胖", "web"}
    
console.log(setArr.has('jspang'));//true
```

- 删除clear: 清除所有成员，没有返回值。

```js
let setArr = new Set(['jspang','技术胖','web','jspang']);
console.log(setArr);//Set {"jspang", "技术胖", "web"}
setArr.clear();
    
console.log(setArray);//true
```


### 3. set的循环

- keys()：返回键名的遍历器。

- values()：返回键值的遍历器。

- entries()：返回键值对的遍历器。

- forEach()：使用回调函数遍历每个成员。

Set遍历顺序是插入顺序，当保存多个回调函数，只需按照顺序调用。但由于Set结构没有键名只有键值，所以keys()和values()是返回结果相同。

```js
let a = new Set(['a','b','c']);
for(let i of a.keys()){console.log(i)};   // 'a' 'b' 'c'
for(let i of a.values()){console.log(i)}; // 'a' 'b' 'c'
for(let i of a.entries()){console.log(i)}; 
// ['a','a'] ['b','b'] ['c','c']
```

#### for…of…循环：
    
```js
let setArr = new Set(['jspang','技术胖','web','jspang']);
for (let item of setArr){
    console.log(item);
}
```

#### size属性: size属性可以获得Set值的数量。

```js
let setArr = new Set(['jspang','技术胖','web','jspang']);
for (let item of setArr){
    console.log(item);
}
    
console.log(setArr.size);
```

#### forEach循环
    
```js
let setArr = new Set(['jspang','技术胖','web','jspang']);
setArr.forEach((value)=>console.log(value));
```

### 4. Set的应用

#### 数组去重：

```js
// 方法1
[...new Set([1,2,3,4,4,4])]; // [1,2,3,4]
// 方法2
Array.from(new Set([1,2,3,4,4,4]));    // [1,2,3,4]
```

#### 遍历和过滤：

```js
let a = new Set([1,2,3,4]);

// map 遍历操作
let b = new Set([...a].map(x =>x*2));// b => Set(4) {2,4,6,8}

// filter 过滤操作
let c = new Set([...a].filter(x =>(x%2) == 0)); // b => Set(2) {2,4}
```

#### 获取并集、交集和差集：

```js
let a = new Set([1,2,3]);
let b = new Set([4,3,2]);

// 并集
let c1 = new Set([...a, ...b]);  // Set {1,2,3,4}

// 交集
let c2 = new Set([...a].filter(x => b.has(x))); // set {2,3}

// 差集
let c3 = new Set([...a].filter(x => !b.has(x))); // set {1}
```


### 5. WeakSet的声明

```js
let weakObj=new WeakSet();
let obj={a:'jspang',b:'技术胖'}
weakObj.add(obj);
 
console.log(weakObj);
```

- 这里需要注意的是，如果你直接在new 的时候就放入值，将报错。

- WeakSet里边的值也是不允许重复的，我们来测试一下。

```js
let weakObj=new WeakSet();
let obj={a:'jspang',b:'技术胖'}
let obj1=obj;
 
weakObj.add(obj);
weakObj.add(obj1);
 
console.log(weakObj);
```

## 第14节：map数据结构: 

由于传统的JavaScript对象只能用字符串当做键，给开发带来很大限制，ES6增加Map数据结构，使得各种类型的值(包括对象)都可以作为键。

Map结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。 基础使用：

```js
let a = new Map();
let b = {name: 'leo' };
a.set(b,'my name'); // 添加值
a.get(b);           // 获取值
a.size;      // 获取总数
a.has(b);    // 查询是否存在
a.delete(b); // 删除一个值
a.clear();   // 清空所有成员 无返回
```

- Map包含键值对。它与数组类似，但我们可以定义自己的索引。索引在Map中是唯一的。

```js
var NewMap = new Map();
NewMap.set('name', 'John'); 
NewMap.set('id', 2345796);
NewMap.set('interest', ['js', 'ruby', 'python']);
NewMap.get('name'); // John
NewMap.get('id'); // 2345796
NewMap.get('interest'); // ['js', 'ruby', 'python']
```

- Map的其他有趣的功能是所有索引都是唯一的。 我们可以使用任何值作为键或值。

```js
var map = new Map();
map.set('name', 'John');
map.set('name', 'Andy');
map.set(1, 'number one');
map.set(NaN, 'No value');
map.get('name'); // Andy. 注意John被Andy替换了.
map.get(1); // number one
map.get(NaN); // No value
```

- Map中另外一些有用的方法：

```js
var map = new Map();
map.set('name', 'John');
map.set('id', 10);
map.size; // 2. 返回map的大小.
map.keys(); // 返回所有的键. 
map.values(); // 返回所有的值.
// map.keys() 返回map的键，但是返回的是一个Iteratord对象，这意味这不能按原样展示出来，只能通过迭代展示出来。
for (let key of map.keys()) {
 console.log(key);
}
输出:
name
id
```
```js
var map = new Map();
for (let element of map) {
 console.log(element);
}
输出:
['name', 'John']
['id', 10]
```

### 1. Json和map格式的对比

- map的效率和灵活性更好

- 先来写一个JSON，这里我们用对象进行模拟操作。

    ```js
    let json = {
        name:'jspang',
        skill:'web'
    }
    console.log(json.name);
    ```

- 但是这种反应的速度要低于数组和map结构。而且Map的灵活性要更好，你可以把它看成一种特殊的键值对，但你的key可以设置成数组，值也可以设置成字符串，让它不规律对应起来。

    ```js
    let json = {
        name:'jspang',
        skill:'web'
    }
    console.log(json.name);
        
    var map=new Map();
    map.set(json,'iam');
    console.log(map);
    ```

- 当然也可key字符串，value是对象。我们调换一下位置，依然是符合map的数据结构规范的。

    ```js
    map.set('jspang',json);
    console.log(map);
    ```

 
### 2. map的增删查

- 取值get: 现在取json对应的值。
    
    ```js
    console.log(map.get(json));
    ```
- 删除delete: 删除delete的特定值

    ```js
    map.delete(json);
    console.log(map)
    ```
- size属性

    ```js
    console.log(map.size);
    ```

- 查找是否存在has

    ```js
    console.log(map.has('jspang'))
    ```

- 清楚所有元素clear

    ```js
    map.clear()
    ```

### 3. Map 的遍历: 顺序就是插入顺序。

- keys()：返回键名的遍历器。

- values()：返回键值的遍历器。

- entries()：返回所有成员的遍历器。

- forEach()：遍历 Map 的所有成员。

```js
let a = new Map([
    ['name','leo'],
    ['age',18]
])

for (let i of a.keys()){...};
for (let i of a.values()){...};
for (let i of a.entries()){...};
a.forEach((v,k,m)=>{
    console.log(`key:${k},value:${v},map:${m}`)
})
```

将Map结构转成数组结构：

```js
let a = new Map([
    ['name','leo'],
    ['age',18]
])

let a1 = [...a.keys()];   // a1 => ["name", "age"]
let a2 = [...a.values()]; // a2 =>  ["leo", 18]
let a3 = [...a.entries()];// a3 => [['name','leo'], ['age',18]]
```

### 4. Map与其他数据结构互相转换

#### Map 转 数组

```js
let a = new Map().set(true,1).set({f:2},['abc']);
[...a]; // [[true:1], [ {f:2},['abc'] ]]
```

#### 数组 转 Map

```js
let a = [ ['name','leo'], [1, 'hi' ]]
let b = new Map(a);
```

#### Map 转 对象

如果所有 Map 的键都是字符串，它可以无损地转为对象。

如果有非字符串的键名，那么这个键名会被转成字符串，再作为对象的键名。

```js
function fun(s) {
  let obj = Object.create(null);
  for (let [k,v] of s) {
    obj[k] = v;
  }
  return obj;
}

const a = new Map().set('yes', true).set('no', false);
fun(a)
// { yes: true, no: false }
```

#### 对象 转 Map

```js
function fun(obj) {
  let a = new Map();
  for (let k of Object.keys(obj)) {
    a.set(k, obj[k]);
  }
  return a;
}

fun({yes: true, no: false})
// Map {"yes" => true, "no" => false}
```

#### Map 转 JSON

(1)Map键名都是字符串，转为对象JSON：

```js
function fun (s) {
    let obj = Object.create(null);
    for (let [k,v] of s) {
        obj[k] = v;
    }
    return JSON.stringify(obj)
}
let a = new Map().set('yes', true).set('no', false);
fun(a);
// '{"yes":true,"no":false}'
```

(2)Map键名有非字符串，转为数组JSON：

```js
function fun (map) {
  return JSON.stringify([...map]);
}

let a = new Map().set(true, 7).set({foo: 3}, ['abc']);
fun(a)
// '[[true,7],[{"foo":3},["abc"]]]'
```

#### JSON 转 Map

(1)所有键名都是字符串：

```js
function fun (s) {
  let strMap = new Map();
  for (let k of Object.keys(s)) {
    strMap.set(k, s[k]);
  }
  return strMap;
  return JSON.parse(strMap);
}
fun('{"yes": true, "no": false}')
// Map {'yes' => true, 'no' => false}
```

(2)整个 JSON 就是一个数组，且每个数组成员本身，又是一个有两个成员的数组:

```js
function fun2(s) {
  return new Map(JSON.parse(s));
}
fun2('[[true,7],[{"foo":3},["abc"]]]')
// Map {true => 7, Object {foo: 3} => ['abc']}
```

## 第15节：用Proxy进行预处理

proxy 用于修改某些操作的默认行为，可以理解为一种拦截外界对目标对象访问的一种机制，从而对外界的访问进行过滤和修改，即代理某些操作，也称“代理器”。

### 1. 声明Proxy

- 我们用new的方法对Proxy进行声明。可以看一下声明Proxy的基本形式。

    ```js
    new Proxy（{},{}）;
    ```

- 需要注意的是这里是两个花括号，第一个花括号就相当于我们方法的主体，后边的花括号就是Proxy代理处理区域，相当于我们写钩子函数的地方。

现在把上边的obj对象改成我们的Proxy形式。

    ```js
    var pro = new Proxy({
        add: function (val) {
            return val + 10;
        },
        name: 'I am Jspang'
    }, {
            get:function(target,key,property){
                console.log('come in Get');
                return target[key];
            }
        });
        
    console.log(pro.name);
    ```

- 可以在控制台看到结果，先输出了come in Get。相当于在方法调用前的钩子函数。

proxy实例化需要传入两个参数，target参数表示所要拦截的目标对象，handler参数也是一个对象，用来定制拦截行为。

```js
let p = new Proxy(target, handler);

let a = new Proxy({}, {
    get: function (target, handler){
        return 'leo';
    }
})
a.name; // leo
a.age;  // leo
a.abcd; // leo
// 上述a实例中，在第二个参数中定义了get方法，来拦截外界访问，并且get方法接收两个参数，分别是目标对象和所要访问的属性，所以不管外部访问对象中任何属性都会执行get方法返回leo。
```
::: tip
只能使用Proxy实例的对象才能使用这些操作。
如果handler没有设置拦截，则直接返回原对象。
:::

### 2. get属性: get属性是在你得到某对象属性值时预处理的方法，他接受三个参数

1. target：得到的目标值

2. key：目标的key值，相当于对象的属性

3. property：这个不太常用，用法还在研究中，还请大神指教。


### 3. set属性: set属性是值你要改变Proxy属性值时，进行的预先处理。它接收四个参数。

1.target:目标值。

2. key：目标的Key值。

3. value：要改变的值。

4. receiver：改变前的原始值。

```js
var pro = new Proxy({
    add: function (val) {
        return val + 10;
    },
    name: 'I am Jspang'
}, {
        get:function(target,key){
            console.log('come in Get');
            return target[key];
        },
        set:function(target,key,value,receiver){
            console.log(`    setting ${key} = ${value}`);
            return target[key] = value;
        }
 
    });
 
console.log(pro.name);
pro.name='技术胖';
console.log(pro.name);
```


### 4. apply的使用: apply的作用是调用内部的方法，它使用在方法体是一个匿名函数时。看下边的代码。

```js
let target = function () {
    return 'I am JSPang';
};
var handler = {
    apply(target, ctx, args) {
        console.log('do apply');
        return Reflect.apply(...arguments);
    }
}
 
var pro = new Proxy(target, handler);
 
console.log(pro());
```

### 5. Proxy支持的13种拦截操作：

- get(target, propKey, receiver)：- 拦截对象属性的读取，比如proxy.foo和proxy['foo']。

- set(target, propKey, value, receiver)：- 拦截对象属性的设置，比如proxy.foo = v或proxy['foo'] = v，返回一个布尔值。

- has(target, propKey)：- 拦截propKey in proxy的操作，返回一个布尔值。

- deleteProperty(target, propKey)：- 拦截delete proxy[propKey]的操作，返回一个布尔值。

- ownKeys(target)：- 拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性。

- getOwnPropertyDescriptor(target, propKey)：- 拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。

- defineProperty(target, propKey, propDesc)：- 拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。

- preventExtensions(target)：- 拦截Object.preventExtensions(proxy)，返回一个布尔值。

- getPrototypeOf(target)：- 拦截Object.getPrototypeOf(proxy)，返回一个对象。

- isExtensible(target)：- 拦截Object.isExtensible(proxy)，返回一个布尔值。

- setPrototypeOf(target, proto)：- 拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。

- apply(target, object, args)：- 拦截 Proxy 实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。

- construct(target, args)：- 拦截 Proxy 实例作为构造函数调用的操作，比如new proxy(...args)。

### 6. 取消Proxy实例

使用Proxy.revocale方法取消Proxy实例。

```js
let a = {};
let b = {};
let {proxy, revoke} = Proxy.revocale(a, b);

proxy.name = 'leo';  // 'leo'
revoeke();
proxy.name;  // TypeError: Revoked
```

### 7. 实现 Web服务的客户端

```js
const service = createWebService('http://le.com/data');
service.employees().than(json =>{
    const employees = JSON.parse(json);
})

function createWebService(url){
    return new Proxy({}, {
        get(target, propKey, receiver{
            return () => httpGet(url+'/'+propKey);
        })
    })
}
```

## 第16节：promise对象：Promise是有助于执行异步操作的对象。

主要用途：**解决异步编程带来的回调地狱问题**。

把<font color=FF0000>Promise</font>简单理解一个容器，存放着某个未来才会结束的事件（通常是一个异步操作）的结果。

通过<font color=FF0000>Promise</font>对象来获取异步操作消息，处理各种异步操作。

- 在Promise之前，程序员习惯于定义回调来处理异步操作。回调是Javascript中的常规函数，它在异步操作完成时执行。

- Promise是ES6中的一个有用功能。它们用于进行异步操作，例如API请求，文件处理，下载图像等。从技术上讲，它们是表示异步操作完成的对象。

### 特点

#### 1. 对象的状态不受外界影响。

>>> Promise对象代表一个异步操作，有三种状态：**pending（进行中）**、**fulfilled（已成功）**和**rejected（已失败）**。只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。这也是Promise这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。

- Promise的生命周期：
    
    1. 挂起：在这种状态下，promise只是执行异步操作。例如，它正在向服务器发出一些API请求或从cdn下载一些图像。 从这个状态Promise可以转移到完成状态或拒绝状态
    
    2. 完成：如果Promise已达到此状态，则表示异步操作已完成，并且得到了输出的结果。例如，我们有了来自API的响应。
    
    3. 拒绝：如果Promise已达到此状态，则表示异步操作未成功，并且我们得到导致操作失败的错误。
```js
// 通过使用new关键字创建构造函数来定义Promise。 然后构造函数将有一个函数（我们称之为执行函数。）
const apiCall = new Promise(function(resolve, reject) {
 // 异步操作在这里定义..
});
```
#### 2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。

>>> Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。如果改变已经发生了，你再对Promise对象添加回调函数，也会立即得到这个结果。这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

### Promise缺点

- 无法取消Promise，一旦新建它就会立即执行，无法中途取消。

- 如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。

- 当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）。

### 基本使用

Promise为一个构造函数，需要用new来实例化。

```js
let p = new Promise(function (resolve, reject){
   if(/*异步操作成功*/){
       resolve(value);
   } else {
       reject(error);
   }
})
```

执行函数有两个参数resolve和reject。
    
1. 第一个参数resolve实际上是一个函数。 它在执行函数内部调用，它表示异步操作成功，我们得到了结果。 resolve函数有助于Promise从挂起状态转为完成状态。

2. 像resolve一样，reject也是一个函数。 它也在执行函数内部调用，它表示异步操作不成功，我们遇到了错误。 reject函数有助于Promise从挂起状态转为拒绝状态。

```js
const apiCall = new Promise(function(resolve, reject) {
 if ( API request to get some data ) {
  resolve("The request is successful and the response is "+ response);
 }
 else {
  reject("The request is not successful. The error is "+error);
 }
});
```

使用处理器来获取promise的输出: 处理器是在某些事件发生时执行的函数，例如单击按钮，移动光标等。

```js
// 调用promise，并使用handlers.
apiCall.then(function(x) {console.log(x); })

// 将一个处理器then附加到promise。处理器then有一个函数参数。函数参数本身有一个参数x。
// 当在promise内调用resolve函数时，处理器then执行其函数参数。
// 输出
The request is successful and the response is {name: "Jon Snow"}

// 同样，还有另一个处理器catch。Catch监听reject函数。
// Catch函数在reject函数被调用时执行其函数参数。
apiCall.then(function(x) {console.log(x); }).catch(function(x) {console.log(x); })
// 假设这个请求没有成功 (在promise中reject函数被调用. )
输出:
The request is not successful

// 最终：
apiCall
.then(function(x) {
 console.log(x); 
})
.catch(function(x) {
 console.log(x);
}) 
```

### 基本方法
    
1. 使用带有函数参数的new关键字定义Promise。 然后函数本身有两个函数参数resolve和reject。

2. 操作成功时应调用resolve函数。

3. 操作失败时应调用reject函数。

4. 处理器then监控resolve函数。
    
作用是为Promise添加状态改变时的回调函数，then方法的第一个参数是resolved状态的回调函数，第二个参数（可选）是rejected状态的回调函数。

then方法返回一个新Promise实例，与原来Promise实例不同，因此可以使用链式写法，上一个then的结果作为下一个then的参数。

```js
getJSON("/posts.json").then(function(json) {
    return json.post;
}).then(function(post) {
// ...
});
```

5. 处理器catch监控reject函数。

Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定发生错误时的回调函数。

```js
getJSON('/posts.json').then(function(posts) {
  // ...
}).catch(function(error) {
  // 处理 getJSON 和 前一个回调函数运行时发生的错误
  console.log('发生错误！', error);
});
```

如果 Promise 状态已经变成resolved，再抛出错误是无效的。

```js
const p = new Promise(function(resolve, reject) {
  resolve('ok');
  throw new Error('test');
});
p
  .then(function(value) { console.log(value) })
  .catch(function(error) { console.log(error) });
// ok
```

> 一般来说，不要在then方法里面定义Reject 状态的回调函数（即then的第二个参数），总是使用catch方法。

6. Promise.prototype.finally()

finally方法用于指定不管 Promise 对象最后状态如何，都会执行的操作。该方法是 ES2018 引入标准的。

```js
promise
.then(result => {···})
.catch(error => {···})
.finally(() => {···});
```
7. Promise.all()
用于将多个 Promise 实例，包装成一个新的 Promise 实例，参数可以不是数组，但必须是Iterator接口，且返回的每个成员都是Promise实例。

```js
const p = Promise.all([p1, p2, p3]);
```

p的状态由p1、p2、p3决定，分成两种情况。
1. 只有p1、p2、p3的状态都变成fulfilled，p的状态才会变成fulfilled，此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。
2. 只要p1、p2、p3之中有一个被rejected，p的状态就变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。

```js
// 生成一个Promise对象的数组
const promises = [2, 3, 5, 7, 11, 13].map(function (id) {
  return getJSON('/post/' + id + ".json");
});

Promise.all(promises).then(function (posts) {
  // ...
}).catch(function(reason){
  // ...
});
```

上面代码中，promises是包含 6 个 Promise 实例的数组，只有这 6 个实例的状态都变成fulfilled，或者其中有一个变为rejected，才会调用Promise.all方法后面的回调函数。

>>> 注意：如果Promise的参数中定义了catch方法，则rejected后不会触发Promise.all()的catch方法，因为参数中的catch方法执行完后也会变成resolved，当Promise.all()方法参数的实例都是resolved时就会调用Promise.all()的then方法。

```js
const p1 = new Promise((resolve, reject) => {
  resolve('hello');
})
.then(result => result)
.catch(e => e);

const p2 = new Promise((resolve, reject) => {
  throw new Error('报错了');
})
.then(result => result)
.catch(e => e);

Promise.all([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));
// ["hello", Error: 报错了]
```

如果参数里面都没有catch方法，就会调用Promise.all()的catch方法。

```js
const p1 = new Promise((resolve, reject) => {
  resolve('hello');
})
.then(result => result);

const p2 = new Promise((resolve, reject) => {
  throw new Error('报错了');
})
.then(result => result);

Promise.all([p1, p2])
.then(result => console.log(result))
.catch(e => console.log(e));
// Error: 报错了
```

8. Promise.race()

与Promise.all方法类似，也是将多个Promise实例包装成一个新的Promise实例。

```js
const p = Promise.race([p1, p2, p3]);
```

与Promise.all方法区别在于，Promise.race方法是p1, p2, p3中只要一个参数先改变状态，就会把这个参数的返回值传给p的回调函数。

9. Promise.resolve()

将现有对象转换成 Promise 对象。

```js
const p = Promise.resolve($.ajax('/whatever.json'));
```

10. Promise.reject()

返回一个rejected状态的Promise实例。

```js
const p = Promise.reject('出错了');
// 等同于
const p = new Promise((resolve, reject) => reject('出错了'))

p.then(null, function (s) {
  console.log(s)
});
// 出错了
```
> 注意，Promise.reject()方法的参数，会原封不动地作为reject的理由，变成后续方法的参数。这一点与Promise.resolve方法不一致。

```js
const thenable = {
  then(resolve, reject) {
    reject('出错了');
  }
};

Promise.reject(thenable)
.catch(e => {
  console.log(e === thenable)
})
// true
```


11. 确保代码的可读性。

```js
var ApiCall = new Promise(function(resolve, reject) {
  
  var request = new XMLHttpRequest();
  request.open('GET', 'https://api.github.com/users/srebalaji');

  request.onload = function() {
    if (request.status == 200) {
      
      resolve(request.response);
    } else {
      reject(Error(request.statusText));
    }
  }

  request.send();
});

ApiCall
.then(function(x) {
  document.getElementById('response').innerHTML = x;
})
.catch(function(x) {
	document.getElementById('response').innerHTML = x;
})
```


promise的基本用法: promise执行异步操作非常好用，那我们就来模仿一个异步操作的过程，那就以吃饭为例吧。要想在家吃顿饭，是要经过三个步骤的。

- 洗菜做饭。
- 坐下来吃饭。
- 收拾桌子洗碗。

- 这个过程是有一定的顺序的，你必须保证上一步完成，才能顺利进行下一步。我们可以在脑海里先想想这样一个简单的过程在ES5写起来就要有多层的嵌套。那我们现在用promise来实现。

```js
let state=1;
    
function step1(resolve,reject){
    console.log('1.开始-洗菜做饭');
    if(state==1){
        resolve('洗菜做饭--完成');
    }else{
        reject('洗菜做饭--出错');
    }
}
    
    
function step2(resolve,reject){
    console.log('2.开始-坐下来吃饭');
    if(state==1){
        resolve('坐下来吃饭--完成');
    }else{
        reject('坐下来吃饭--出错');
    }
}
    
    
function step3(resolve,reject){
    console.log('3.开始-收拾桌子洗完');
        if(state==1){
        resolve('收拾桌子洗完--完成');
    }else{
        reject('收拾桌子洗完--出错');
    }
}
    
new Promise(step1).then(function(val){
    console.log(val);
    return new Promise(step2);
    
}).then(function(val){
        console.log(val);
    return new Promise(step3);
}).then(function(val){
    console.log(val);
    return val;
});
```

## 第17节：class类的使用

1. 类的声明

- 先声明一个最简单的coder类，类里只有一个name方法，方法中打印出传递的参数。

```js
class coder{
    name(val){
        console.log(val);
    }
}
```

2. 类的使用

- 我们已经声明了一个类，并在类里声明了name方法，现在要实例化类，并使用类中的方法。

```js
class Coder{
    name(val){
        console.log(val);
    }
}
 
let jspang= new Coder;
jspang.name('jspang');
```

3. 类的多方法声明

```js
class Coder{
    name(val){
        console.log(val);
        return val;
    }
    skill(val){
        console.log(this.name('jspang')+':'+'Skill:'+val);
    }
}
 
let jspang= new Coder;
jspang.name('jspang');
jspang.skill('web');
```
- 这里需要注意的是两个方法中间不要写逗号了，还有这里的this指类本身，还有要注意return 的用法。

4. 类的传参

- 在类的参数传递中我们用constructor( )进行传参。传递参数后可以直接使用this.xxx进行调用。

```js
class Coder{
    name(val){
        console.log(val);
        return val;
    }
    skill(val){
        console.log(this.name('jspang')+':'+'Skill:'+val);
    }
 
    constructor(a,b){
        this.a=a;
        this.b=b;
    }
 
    add(){
        return this.a+this.b;
    }
}
 
let jspang=new Coder(1,2);
console.log(jspang.add());
```


- 我们用constructor来约定了传递参数，然后用作了一个add方法，把参数相加。这和以前我们的传递方法有些不一样，所以需要小伙伴们多注意下。

5. class的继承

- 如果你学过java，一定知道类的一大特点就是继承。ES6中也就继承，在这里我们简单的看看继承的用法。

```js
class htmler extends Coder{}
let pang=new htmler;
pang.name('技术胖');
```
声明一个htmler的新类并继承Coder类，htmler新类里边为空，这时候我们实例化新类，并调用里边的name方法。结果也是可以调用到的。

- Extend用于从父类创建子类。子类继承了父类的所有属性，还可以修改父类的属性。

```js
// 使用构造函数和简单方法定义了一个Person类。
class Person{
 constructor(firstName, lastName, age) {
   this.firstName = firstName;
   this.lastName = lastName;
   this.age = age;
 }
 displayName() {
  return `${this.firstName} - ${this.lastName}`;
 }
}
// 定义了另一个类Employee，它是一个继承自Person的子类。我们使用extend来实现这一目标。
class Employee extends Person {
 constructor(firstName, lastName, age, salary) {
  // 然后我们使用super关键字来调用父类的构造函数。我们还使用super调用父类中声明的方法。
  // 只有在调用super之后才能在子类中使用this。
  // 如果在子类中调用super之前使用this，则会得到RefrenceError。
  super(firstName, lastName, age);
  this.salary = salary;
 }
 displaySalary() {
  return `${this.salary}`;
 }
 displayName() {
  return super.displayName();
 }
 displayAge() {
  return this.age;
 }
}
let manager = new Employee("Jon", "Snow", 23, 100);
console.log(manager.displaySalary());
console.log(manager.displayName());
console.log(manager.displayAge());
输出:
100
Jon Snow
23
```
1、我们使用extends从父类创建一个子类。 
2、我们用super来调用父类的构造函数。 
3、我们使用super来调用父类中定义的方法。 

6. 静态方法

```js
class Example {
 static Callme() {
 console.log("Static method");
 }
}
Example.Callme();
输出:
Static method
```

- 可以在不为类创建任何实例的情况下调用该函数。

7. Getters和Setters

- Getters和Setterss是ES6中引入的有用功能之一。 如果你在JS中使用类，它会派上用场。

```js
// 没有getter和setter的示例：
class People {
constructor(name) {
 this.name = name;
 }
 getName() {
 return this.name;
 }
 setName(name) {
 this.name = name;
 }
}
let person = new People("Jon Snow");
console.log(person.getName());
person.setName("Dany");
console.log(person.getName());
输出:
Jon Snow
Dany

// 上面的例子不言自明. 在类People中，我们有两个函数帮助我们设置和获取一个人的名字。

// getters 和 setters的例子：
class People {
constructor(name) {
 this.name = name;
 }
 get Name() {
 return this.name;
 }
 set Name(name) {
 this.name = name;
 }
}
let person = new People("Jon Snow");
console.log(person.Name);
person.Name = "Dany";
console.log(person.Name);
```
- 在上面的示例中，您可以看到在People类中，有两个函数分别具有'get'和'set'属性， 'get'属性用于获取变量的值，'set'属性用于设置变量的值。

- 你可以看到调用getName函数并没有使用括号， 并且调用setName函数也没有使用括号，就像为变量赋值一样。

## 第18节：模块化操作(导入和导出)
- 在ES5中我们要进行模块华操作需要引入第三方类库，随着前后端分离，前端的业务日渐复杂，ES6为我们增加了模块话操作。模块化操作主要包括两个方面。

    1. export :负责进行模块化，也是模块的输出。
    
    2. import : 负责把模块引，也是模块的引入操作。

1. export的用法：

    - export可以让我们把变量，函数，对象进行模块话，提供外部调用接口，让外部进行引用。先来看个最简单的例子，把一个变量模块化。我们新建一个temp.js文件，然后在文件中输出一个模块变量。

    ```js
    export var a = 'jspang';
    ```
    - 然后可以在index.js中以import的形式引入。

    ```js
    import {a} from './temp.js';
    
    console.log(a);
    ```

    - 这就是一个最简单的模块的输出和引入。

    2. 多变量的输出

    - 这里声明了3个变量，需要把这3个变量都进行模块化输出，这时候我们给他们包装成对象就可以了。

    ```js
    var a ='jspang';
    var b ='技术胖';
    var c = 'web';
    
    export {a,b,c}
    ```


    3. 函数的模块化输出

    ```js
    export function add(a,b){
        return a+b;
    }
    ```

    4. as的用法

    - 有些时候我们并不想暴露模块里边的变量名称，而给模块起一个更语义话的名称，这时候我们就可以使用as来操作。

    ```js
    var a ='jspang';
    var b ='技术胖';
    var c = 'web';
    
    export {
        x as a,
        y as b,
        z as c
    }
    ```

    5. export default的使用

    - 加上default相当是一个默认的入口。在一个文件里export default只能有一个。我们来对比一下export和export default的区别

    1. export
        - 可导入多个
        
        ```
        export var a ='jspang';
        
        export function add(a,b){
            return a+b;
        }
        ```
        - 对应的导入方式

        ```
        import {a,add} form './temp';//也可以分开写
        ```
    2. export defalut

        
        - 一个文件里export default只能有一个
        
        ```js
        export default var a='jspang';
        ```

        - 对应的引入方式：可以自定义引入的名字

        ```js
        import str from './temp';
        ```

2. import的用法：
    1. 如果使用*来导入值，则必须使用别名（也就是）引用导入的所有的值。在我们的示例中，我们使用variables作为别名。
    
    ```js
    app.js
    let a = 10;
    let b = 2;
    let sum = () => a+b;
    export {a,b}
    export default sum
    index.js
    import * as variables from './app'
    import addition from './app' // default value
    console.log(variables.a);
    console.log(variables.b);
    console.log(addition());
    输出:
    10
    2
    12
    ```

    2. 使用*导入值不会导入默认值。你必须单独导入它。

    - 如果需要在一行中导入默认值和其他值:
    ```js
    import addition, * as variables from './app'
    ```


## 第19节. Async / Await

### Async: Async关键字使任何函数只返回promises。

```js
// eg
async function hello() {
 return "Hello Promise..!"
}
// 函数hello将返回一个promise。

// 相当于
function hello() {
 return new Promise(function(resolve, reject) {
 // executor function body
 });
}
```
```js
async function hello(a, b) {
 if (a < b) {
  return "Greater";
 }
 else {
  return new Error("Not Greater");
 }
}
hello(14, 10)
.then(function(x) {
 console.log("Good..! " + x); 
})
.catch(function(x) {
 console.log("Oops..! " + x); 
})
输出:
Oops..! Not Greater. 
// 如果你调用 hello(4, 10) 你会得到 "Good..! Greater"
```
在上面的代码中，我们定义了一个async函数并返回了一些值或返回了一些错误。

如果要在async函数中返回一些值，则它等同于调用resolve函数。

如果通过使用'new'调用错误构造函数（即）返回一些错误，则它等同于reject函数。

不要忘记async函数将返回一个promise。 当然，你也可以在async函数中调用resolve和reject函数。

```js
async function Max(a, b) {
 if (a > b) {
  return Promise.resolve("Success");
 }
 else {
  return Promise.reject("Error");
 }
}
Max(4, 10)
.then(function(x) {
 console.log("Good " + x); 
})
.catch(function(x) {
 console.log("Oops " + x); 
});
输出:
Oops Error
// 如果调用 Max(14, 10) 我们会得到 "Good Success" :)
```

### Await

- 顾名思义，它使Javascript等到操作完成。 假设您正在使用await关键字发出API请求。 它使Javascript等待，直到您从端点获得响应。 然后它恢复执行。

- Await只能在异步函数中使用。 它在异步功能之外不起作用

```js
async function hello() {
 let response = await fetch('https://api.github.com/');
 // 上面一行从给定的API终端获取响应
 return response;
}
hello()
.then(function(x) {
 console.log(x); 
});
...
...
输出:
Response from the API.
```
await操作仅停止hello函数内的执行。 hello函数外的其余代码不会受到影响。 执行在函数外部继续。 当我们得到响应时，执行内部函数参数。

- 例子

```js
function getResponse() {
  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      resolve("Response from API. Executed after 5 secs");
    }, 5000);
  });
}

async function hello() {
  let response = await getResponse();
  return response;
}

hello()
  .then(function(x) {
    console.log(x);
  })
  .catch(function(x) {
    console.log(x);
  });
console.log("Im executed before getResponse()");
```

我们对getResponse函数使用了await。 并且getResponse将在5秒后返回输出或错误。 因此，在此之前，执行将暂停，然后返回响应。

- 实例

```js
function getResponse(url) {
	return new Promise(function(success, failure) {
  var request = new XMLHttpRequest();
	request.open('GET', url);
	
  request.onload = function() {
    if (request.status == 200) {
      return success(request.response);
    } else {
      return failure("Error in processing..!" + request.status);
    }
  }
  request.onerror = function() {
    return failure("Error in processing ");
  }
  request.send();
  });
}

function getUsername(response) {
  response = JSON.parse(response);
  return response["login"];
}

function makeUsernameCaps(name) {
	return new Promise(function(success, failure) {
  	// Let's assume it takes 3secs to make the username caps :) 
  	setTimeout(function() {
    success(name.toUpperCase());
    }, 3000)
  });
}
async function apiCall(url) {
  let response = await getResponse(url); 
  let username = await getUsername(response);
  let username_in_caps = await makeUsernameCaps(username);
  return username_in_caps;
}

apiCall("https://api.github.com/users/srebalaji")
.then(function(x) {
	console.log(x);
})
.catch(function(x) {
	console.log("Error - "+x);
});
```
我们已经使用了多个await。 因此，对于每个await, 程序停止执行，直到收到响应然后恢复。

在示例中尝试使用一些无效网址。 您可以看到引发错误。

- async函数中的错误处理非常简单。 如果在async函数内引发错误，或者在async函数中使用await调用的其他函数内引发错误，则会调用reject函数。

## 第20节. 正则的拓展

第一个参数是正则对象，第二个是指定修饰符，如果第一个参数已经有修饰符，则会被第二个参数覆盖。

```js
new RegExp(/abc/ig, 'i');
```

### 字符串的正则方法

常用的四种方法：

- match()

- replace()

- search()

- split()

### u修饰符

添加u修饰符，是为了处理大于uFFFF的Unicode字符，即正确处理四个字节的UTF-16编码。

```js
/^\uD83D/u.test('\uD83D\uDC2A'); // false
/^\uD83D/.test('\uD83D\uDC2A');  // true
```
由于ES5之前不支持四个字节UTF-16编码，会识别为两个字符，导致第二行输出true，加入u修饰符后ES6就会识别为一个字符，所以输出false。

> 加上u修饰符后，会改变下面正则表达式的行为：

- (1)点字符 点字符(.)在正则中表示除了换行符以外的任意单个字符。对于码点大于0xFFFF的Unicode字符，点字符不能识别，必须加上u修饰符。

```js
var a = "𠮷";
/^.$/.test(a);  // false
/^.$/u.test(a); // true
```

- (2)Unicode字符表示法 使用ES6新增的大括号表示Unicode字符时，必须在表达式添加u修饰符，才能识别大括号。

```js
/\u{61}/.test('a');      // false
/\u{61}/u.test('a');     // true
/\u{20BB7}/u.test('𠮷'); // true
```

- (3)量词 使用u修饰符后，所有量词都会正确识别码点大于0xFFFF的 Unicode 字符。

```js
/a{2}/.test('aa');    // true
/a{2}/u.test('aa');   // true
/𠮷{2}/.test('𠮷𠮷');  // false
/𠮷{2}/u.test('𠮷𠮷'); // true
```

- (4)i修饰符 不加u修饰符，就无法识别非规范的K字符。

```js
/[a-z]/i.test('\u212A') // false
/[a-z]/iu.test('\u212A') // true
```

检查是否设置u修饰符： 使用unicode属性。

```js
const a = /hello/;
const b = /hello/u;

a.unicode // false
b.unicode // true
```

### y修饰符

y修饰符与g修饰符类似，也是全局匹配，后一次匹配都是从上一次匹配成功的下一个位置开始。区别在于，g修饰符只要剩余位置中存在匹配即可，而y修饰符是必须从剩余第一个开始。

```js
var s = 'aaa_aa_a';
var r1 = /a+/g;
var r2 = /a+/y;

r1.exec(s) // ["aaa"]
r2.exec(s) // ["aaa"]

r1.exec(s) // ["aa"]  剩余 '_aa_a'
r2.exec(s) // null
```

- lastIndex属性: 指定匹配的开始位置：

```js
const a = /a/y;
a.lastIndex = 2;  // 从2号位置开始匹配
a.exec('wahaha'); // null
a.lastIndex = 3;  // 从3号位置开始匹配
let c = a.exec('wahaha');
c.index;          // 3
a.lastIndex;      // 4
```

- 返回多个匹配：一个y修饰符对match方法只能返回第一个匹配，与g修饰符搭配能返回所有匹配。

```js
'a1a2a3'.match(/a\d/y);  // ["a1"]
'a1a2a3'.match(/a\d/gy); // ["a1", "a2", "a3"]
```

检查是否使用y修饰符：使用sticky属性检查。

```js
const a = /hello\d/y;
a.sticky;     // true
```

### flags属性

flags属性返回所有正则表达式的修饰符。

```js
/abc/ig.flags;  // 'gi'
```

