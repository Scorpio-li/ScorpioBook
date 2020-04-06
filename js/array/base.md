# 数组基本操作

## 0. length属性：直接给Array的length赋值会导致Array大小的变化

```js
var arr = [1, 2, 3]; 
arr.length; // 3
arr.length = 6;
arr; // arr变为[1, 2, 3, undefined, undefined, undefined]
arr.length = 2;
arr; // arr变为[1, 2]
```

## 1. unshift和shift:如果要往Array的头部添加若干元素，使用unshift()方法，shift()方法则把Array的第一个元素删掉

```js
var arr = [1, 2];
arr.unshift('A', 'B'); // 返回Array新的长度: 4
arr; // ['A', 'B', 1, 2]
arr.shift(); // 'A'
arr; // ['B', 1, 2]
arr.shift(); arr.shift(); arr.shift(); // 连续shift 3次
arr; // []
arr.shift(); // 空数组继续shift不会报错，而是返回undefined
arr; // []
```

### shift() 方法：把数组的第一个元素删除，并返回第一个元素的值

```js
var movePos=[1,2];

movePos.shift()

console.log(movePos)//[2]

document.write(movePos.length);//1
```

### unshift：将参数添加到原数组开头，并返回数组的长度 

```js
var movePos =[111,222,333,444];

var arr = movePos.unshift("55555")
document.write(arr);//5
document.write(movePos + "<br />");//55555,111,222,333,444
```

## 2. concat() 方法：用于连接两个或多个数组,并返回一个新数组，新数组是将参数添加到原数组中构成的 

```js
var arr1 = [7,8];
var arr2 = ['1',2,4,5];
var arr3 = ['asdfas'];
var arr = arr1.concat(arr3,arr2);//[7, 8, "asdfas", "1", 2, 4, 5]
```

- concat()方法并没有修改当前Array，而是返回了一个新的Array

- 实际上，concat()方法可以接收任意个元素和Array，并且自动把Array拆开，然后全部添加到新的Array里

```js
var arr = ['A', 'B', 'C'];
arr.concat(1, 2, [3, 4]); // ['A', 'B', 'C', 1, 2, 3, 4]
```

## 3. join() 方法：用于把数组中的所有元素放入一个字符串。元素是通过指定的分隔符进行分隔的。

- 返回一个字符串。该字符串是通过把 arrayObject 的每个元素转换为字符串，然后把这些字符串连接起来，在两个元素之间插入separator 字符串而生成的。

```js
var movePos=[11,22];

var arr=movePos.join("+");

document.write(arr) //11+22
```

## 4. push和pop: 如果要往Array的尾部添加若干元素，使用push()方法，pop()方法则把Array的最后一个元素删掉

### pop() 方法：用于删除并返回数组的最后一个(删除元素)元素,如果数组为空则返回undefined ,把数组长度减 1

```js
var movePos = [11,22,33];
var arr = movPos.pop();
document.write(arr);//33
document.write(movPos.length);//2
```

### push() 方法：可向数组的末尾添加一个或多个元素，并返回新的长度，（用来改变数组长度）。

```js
var movPos = [11,22];
var arr = movPos.push("33");
console.log(arr);//3
console.log(movPos);//[11, 22, "33"]
console.log(arr.length);
```

## 5. reverse() ：方法用于颠倒数组中元素的顺序,并返回新的数组。

```js
var arr = ['one', 'two', 'three'];
arr.reverse(); 
arr; // ['three', 'two', 'one']
```

## 6. slice() 方法：截取Array的部分元素，然后返回一个新的Array。slice(开始截取位置，结束截取位置)

```js
var arr = ['A', 'B', 'C', 'D', 'E', 'F', 'G'];
arr.slice(0, 3); // 从索引0开始，到索引3结束，但不包括索引3: ['A', 'B', 'C']
arr.slice(3); // 从索引3开始到结束: ['D', 'E', 'F', 'G']
```

- 如果不给slice()传递任何参数，它就会从头到尾截取所有元素。


## 7. splice() ：方法向/从数组中添加/删除项目，然后返回被删除的项目。

```js
// splice() 方法可删除从index处开始的零个或多个元素，并且用参数列表中声明的一个或多个值来替换那些被删除的元素。
var movePos =[111,222,333,444];
movePos.splice(2,1,"666")//movePos.splice(开始删除的下表位置,删除数组元素的个数，向数组添加的新项目。);从下标2开始删除一位，并用666替换删除下表位置的元素
document.write(movePos + "<br />")

var arr = ['Microsoft', 'Apple', 'Yahoo', 'AOL', 'Excite', 'Oracle'];
// 从索引2开始删除3个元素,然后再添加两个元素:
arr.splice(2, 3, 'Google', 'Facebook'); // 返回删除的元素 ['Yahoo', 'AOL', 'Excite']
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
// 只删除,不添加:
arr.splice(2, 2); // ['Google', 'Facebook']
arr; // ['Microsoft', 'Apple', 'Oracle']
// 只添加,不删除:
arr.splice(2, 0, 'Google', 'Facebook'); // 返回[],因为没有删除任何元素
arr; // ['Microsoft', 'Apple', 'Google', 'Facebook', 'Oracle']
```

## 8. sort(orderfunction)：按指定的参数对数组进行排序 

- sort()方法接受一个比较函数的参数，根据比较函数的返回值确定排序。如果不传入比较函数，JavaScript会先将数组的元素转换为字符串类型，并依照ASCII码的值升序排列。

```
var array = [1,2,3,4,11];
console.log(array.sort().toString());//1,11,2,3,4
```
- 传入比较函数参数时，若比较函数返回的值为true则交换两个元素的位置，否则不交换

```
var array = [1,2,3,4,11];
console.log(array.sort(function(a,b){return a-b}).toString());//1,2,3,4,11
```
```js
function (a,b){
    return a-b;//升序
    return b-a;//降序
}
```

## 9. indexOf：通过indexOf()来搜索一个指定的元素的位置

- .indexOf()能够告诉你 某个元素在数组中的位置，它返回的是索引值，如果数组里有重复的元素，它会返回第一个元素的位置。

- 传参：元素。返回：该元素的下标，若没有该元素返回-1。

```js
var arr = [10, 20, '30', 'xyz'];
arr.indexOf(10); // 元素10的索引为0
arr.indexOf(20); // 元素20的索引为1
arr.indexOf(30); // 元素30没有找到，返回-1
arr.indexOf('30'); // 元素'30'的索引为2
```