# JavaScript 的对象

对象是多个属性的动态集合，它有一个链接着原型的隐藏属性（注：<font color=FF0000>__proto__</font>）。

一个属性拥有一个 key 和一个 value 。


## 属性的 key

属性的 key 是一个唯一的字符串。

访问方式：

- 点表示法： 属性的 key 必须是有效的标识符。

- 括号表示法：属性的 key 不要求是有效的标识符 —— 可以是任意值。

```js
let obj = {
  message : "A message"
}
obj.message //"A message"
obj["message"] //"A message"
```

当属性的key是一个非字符串的值，会用toString()方法（如果可用的话）把它转换为字符串。

```js
let obj = {};
//Number
obj[1] = "Number 1";
obj[1] === obj["1"]; //true
//Object
let number1 = {
  toString : function() { return "1"; }
}
obj[number1] === obj["1"]; //true
// 对象 number1 被用作一个 key 。它会被转换为字符串，转换结果 “1” 被用作属性的 key 。
```

## 属性的值

> 属性的值可以是任意的基础数据类型，对象，或函数。

## 动态性

对象本质上就是动态的。可以任意添加删除属性。

```js
let obj = {};
obj.message = "This is a message"; //add new property
obj.otherMessage = "A new message"; //add new property
delete obj.otherMessage; //delete property
```

## 原型

对象有一个链接着原型对象的“隐藏”属性 __proto__，对象是从这个原型对象中继承属性的。

举个例子，使用对象字面量创建的对象有一个指向 <font color=FF0000>Object.prototype</font> 的链接:

```js
var obj = {};
obj.__proto__ === Object.prototype; //true
```

### 原型链

原型对象有它自己的原型。当一个属性被访问的时候并且不包含在当前对象中，JavaScript会沿着原型链向下查找直到找到被访问的属性，或者到达 null 为止。

### 只读

原型只用于读取值。对象进行更改时，只会作用到当前对象，不会影响对象的原型；就算原型上有同名的属性，也是如此。

### 空对象

正如我们看到的，空对象 {} 并不是真正意义上的空，因为它包含着指向 <font color=FF0000>Object.prototype</font> 的链接。为了创建一个真正的空对象，我们可以使用 <font color=FF0000>Object.create(null)</font> 。它会创建一个没有任何属性的对象。这通常用来创建一个Map。

## 原始值和包装对象

在允许访问属性这一点上，JavaScript 把原始值描述为对象。当然了，原始值并不是对象。

```js
(1.23).toFixed(1); //"1.2"
"text".toUpperCase(); //"TEXT"
true.toString(); //"true"
```

为了允许访问原始值的属性， JavaScript 创造了一个包装对象，然后销毁它。JavaScript引擎对创建包装和销毁包装对象的过程做了优化。

数值、字符串和布尔值都有等效的包装对象。跟别是：<font color=FF0000>Number、String、Boolean</font>。

<font color=FF0000>null 和 undefined</font> 原始值没有相应的包装对象并且不提供任何方法。

## 内置原型

Numbers 继承自<font color=FF0000>Number.prototype，Number.prototype</font>继承自<font color=FF0000>Object.prototype</font>。

```js
var no = 1;
no.__proto__ === Number.prototype; //true
no.__proto__.__proto__ === Object.prototype; //true
```

Strings 继承自 <font color=FF0000>String.prototype</font>。Booleans 继承自 <font color=FF0000>Boolean.prototype</font>

函数都是对象，继承自 <font color=FF0000>Function.prototype</font> 。函数拥有 <font color=FF0000>bind()、apply() 和 call()</font> 等方法。

所有对象、函数和原始值（除了 null 和 undefined ）都从 <font color=FF0000>Object.prototype</font> 继承属性。他们都有 <font color=FF0000>toString()</font> 方法。


## 继承

### 单一继承

<font color=FF0000>Object.create()</font> 用特定的原型对象创建一个新对象。它用来做单一继承。

```js
let bookPrototype = {
  getFullTitle : function(){
    return this.title + " by " + this.author;
  }
}
let book = Object.create(bookPrototype);
book.title = "JavaScript: The Good Parts";
book.author = "Douglas Crockford";
book.getFullTitle();//JavaScript: The Good Parts by Douglas Crockford
```

### 多重继承

<font color=FF0000>Object.assign()</font> 从一个或多个对象拷贝属性到目标对象。它用来做多重继承。看下面的例子:

```js
let authorDataService = { getAuthors : function() {} };
let bookDataService = { getBooks : function() {} };
let userDataService = { getUsers : function() {} };
let dataService = Object.assign({},
 authorDataService,
 bookDataService,
 userDataService
);
dataService.getAuthors();
dataService.getBooks();
dataService.getUsers();
```


## 方法

### 不可变对象

<font color=FF0000>Object.freeze()</font> 冻结一个对象。属性不能被添加、删除、更改。对象会变成不可变的。

```js
"use strict";
let book = Object.freeze({
  title : "Functional-Light JavaScript",
  author : "Kyle Simpson"
});
book.title = "Other title";//Cannot assign to read only property 'title'
```

Object.freeze() 实行浅冻结。要深冻结，需要递归冻结对象的每一个属性。


### 拷贝

<font color=FF0000>Object.assign()</font> 被用作拷贝对象。

```js
let book = Object.freeze({
  title : "JavaScript Allongé",
  author : "Reginald Braithwaite"
});
let clone = Object.assign({}, book);
```

Object.assign() 执行浅拷贝，不是深拷贝。它拷贝对象的第一层属性。嵌套的对象会在原始对象和副本对象之间共享。

