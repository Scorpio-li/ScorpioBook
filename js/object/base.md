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