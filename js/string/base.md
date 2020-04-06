# 字符串基本操作

## 1.字符串索引：要获取字符串某个指定位置的字符，使用类似Array的下标操作，索引号从0开始

```js
var s = 'Hello, world!';

s[0]; // 'H'
s[6]; // ' '
s[7]; // 'w'
s[12]; // '!'
s[13]; // undefined 超出范围的索引不会报错，但一律返回undefined
```

- 需要特别注意的是，字符串是不可变的，如果对字符串的某个索引赋值，不会有任何错误，但是，也没有任何效果：

```
var s = 'Test';
s[0] = 'X';
alert(s); // s仍然为'Test'
```

## 2.toUpperCase：toUpperCase()把一个字符串全部变为大写

## 3.toLowerCase：toLowerCase()把一个字符串全部变为小写

## 4.indexOf：indexOf()会搜索指定字符串出现的位置，<br/>lastIndexOf():从后向前搜索字符串
        
```js
var s = 'hello, world';
s.indexOf('world'); // 返回7
s.indexOf('World'); // 没有找到指定的子串，返回-1
var str = "abac_dfra_wa";
console.log(str.lastIndexOf('ac')); //输出2
```


## 5.substring()、substr()和slice() （数组中也有此方法）：substring()和slice()返回指定索引区间的子串,substr()指定子字符串的开始位置，返回的子字符串的字符个数，创建新的字符串

```js
var stringValue = "hello world"; 
alert(stringValue.slice(3));          //"lo world" 
alert(stringValue.substring(3));      //"lo world" 
alert(stringValue.substr(3));         //"lo world" 
alert(stringValue.slice(3, 7));       //"lo w" 
alert(stringValue.substring(3,7));    //"lo w" 
alert(stringValue.substr(3, 7));      //"lo worl" 
/*repeat()*/
var a = 'he';
var b = a.repeat(3);
console.log(`${a}---${b}`); /		  //"he---hehehe"
```

## repeat():将原字符串重复n次,如果传入负数，则报错，传入小数和NaN等同于传入0.

- 当给这三个方法传入负值的时候，三个的表现不同：
    1. slice()会将传入的负值与字符串的长度相加
    
    2. substr()会将第一个位置的负值参数加上字符串长度后转为正数，而第二个位置的负值将转化为0
    
    3. substring()会把所有的负参数转化为0
    
    4. repeat()会报错


## 6.charAt():返回在指定位置的字符

```js
var str = "abac_dfra_wa";
console.log(str.charAt(3)); //输出 c

```

## 7.charCodeAt():返回在指定位置的字符的Unicode编码

```js
var str = "abac_dfra_wa";
console.log(str.charCodeAt(3)); //输出99

```

## 8.fromCharCode():从字符编码创建一个字符串。

```js
console.log(String.fromCharCode(72,69,76,76,79)); //输出HELLO

```

## 9.concat()（数组中也有该方法）:连接字符串，生成一个新的字符串

```js
var str = "abac_dfra_wa";
console.log(str.concat('_000')); //输出abac_dfra_wa_000

```
## 10.match():找到一个或多个正则表达式的匹配。

```js
var str="1 plus 2 equal 3"
console.log(str.match('plus')); // plus
console.log(str.match('st'));   // null
console.log(str.match(/\d+/g))  // [ '1', '2', '3' ]

```
## 11.replace()：替换与正则表达式匹配的字符串

```js
var str="Hello WoRlD!"
console.log(str.replace(/WoRlD/, "World"));     // Hello World!

var str="Hello WoRlD! "
str += str;
console.log(str.replace(/WoRlD/g, "World")); //替换所有, 输出：Hello World! Hello World! 

var str = "javascript Tutorial ";
console.log(str.replace(/javascript/i, "JavaScript")); //确保匹配字符串大写字符的正确

var name = "Doe, John";
console.log(name.replace(/(\w+)\s*, \s*(\w+)/, "$2 $1")); //将把 "Doe, John" 转换为 "John Doe" 的形式
```
## 12.search():检索与正则表达式相匹配的值(大小写敏感)，未找到输出-1。

```js
var str="Hello World!"
console.log(str.search(/World/)); //输出6

var str="Hello World!"
console.log(str.search(/world/i)); //忽略大小写的检索，输出6
```



## 13.split():把字符串分割为字符串数组。

```js
"|a|b|c".split("|") ////将返回["", "a", "b", "c"]

"How are you doing today?".split(" ",3) //返回 How,are,you

"hello".split("")	//可返回 ["h", "e", "l", "l", "o"]

```
## 14.includes()、startsWith()、endsWith()

- includes()：返回布尔值，表示是否找到了参数字符串

- startsWith()：返回布尔值，表示参数字符串是否在源字符串的头部

- endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部


```js
var s = 'Hello world';
s.startsWith('world',6);	// true
s.endsWith('Hello',5);		// true
s.includes('Hello',6);		//false
```
- 使用第2个参数n时，endsWith的行为与其他两个方法有所不同。它针对前面n个字符，而其他两个方法针对从第n个位置开始直到字符串结束的字符。

## 15.去空格–trim():ES5中新增trim()方法用于去除字符串的左右空格，该方法会创建一个字符串的副本，不会改变原有的字符串

```js
/*trim	去掉空白
str要处理的字符串		
[type] 	类型：l 去除左边的空白	r去除右边空白	b去掉两边的空白		a去除所有空白*/
function trim (str,type) {
	var type=type||"b";
	if(type=="b"){
		return str.replace(/^\s*|\s*$/g,"");
	}else if(type=="l"){
		return str.replace(/^\s*/g,"");
	}else if(type=="r"){
		return str.replace(/\s*$/g,"");
	}else if(type=="a"){
		return str.replace(/\s*/g,"");
	}
}
```
## 16.localeCompare():用于比较两个字符串，并返回下列值中的一个：

- 如果字符串在字母表中应该排在字符串参数之前，则返回负数（大多情况下为-1）

- 如果相等，则返回0

- 如果排在字符串参数之前，则返回正数（大多数情况下为1）