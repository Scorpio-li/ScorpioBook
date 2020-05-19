# 一. 数组判断：两个相同的数组比较，因为两个单独的数组永不相等

```js
var arr = [],
    arr2 = [];

console.log(arr === arr2); // false

//数组、对象的类型都为object
var arr = [],
    arr2 = {};
    
console.log(typeof(arr) === typeof(arr2)); // true
```

# 二. 数组去重

## 1. 原始方法：双层循环

```js
var array = [1, 1, '1', '1'];

function unique(array) {
    // res用来存储结果
    var res = [];
    for (var i = 0, arrayLen = array.length; i < arrayLen; i++) {
        for (var j = 0, resLen = res.length; j < resLen; j++ ) {
            if (array[i] === res[j]) {
                break;
            }
        }
        // 如果array[i]是唯一的，那么执行完循环，j等于resLen
        if (j === resLen) {
            res.push(array[i])
        }
    }
    return res;
}

console.log(unique(array)); // [1, "1"]

```
- 简化版：使用 indexOf 来循环判断一遍

```js
var array = [1, 1, '1'];

function unique(array) {
    var res = [];
    for (var i = 0, len = array.length; i < len; i++) {
        var current = array[i];
        if (res.indexOf(current) === -1) {
            res.push(current)
        }
    }
    return res;
}

//使用ES5的filter方法：简化外部循环
function unique(array) {
    var res = array.filter(function(item, index, array){
        return array.indexOf(item) === index;
    })
    return res;
}

console.log(unique(array));
```

## 2. 排序后去重
- 相同的值就会被排在一起，然后我们就可以只判断当前元素与上一个元素是否相同，相同就说明重复，不相同就添加进 res

```js
var array = [1, 1, '1'];

function unique(array) {
    var res = [];
    var sortedArray = array.concat().sort();
    var seen;
    for (var i = 0, len = sortedArray.length; i < len; i++) {
        // 如果是第一个元素或者相邻的元素不相同
        if (!i || seen !== sortedArray[i]) {
            res.push(sortedArray[i])
        }
        seen = sortedArray[i];
    }
    return res;
}
//使用ES5的filter方法：简化外部循环
function unique(array) {
    return array.concat().sort().filter(function(item, index, array){
        return !index || item !== array[index - 1]
    })
}

console.log(unique(array));
```

## 3. 综合前两者
- unique 的工具函数，我们根据一个参数 isSorted 判断传入的数组是否是已排序的，如果为 true，我们就判断相邻元素是否相同，如果为 false，我们就使用 indexOf 进行判断

```js
var array1 = [1, 2, '1', 2, 1];
var array2 = [1, 1, '1', 2, 2];

// 第一版
function unique(array, isSorted) {
    var res = [];
    var seen = [];

    for (var i = 0, len = array.length; i < len; i++) {
        var value = array[i];
        if (isSorted) {
            if (!i || seen !== value) {
                res.push(value)
            }
            seen = value;
        }
        else if (res.indexOf(value) === -1) {
            res.push(value);
        }        
    }
    return res;
}

console.log(unique(array1)); // [1, 2, "1"]
console.log(unique(array2, true)); // [1, "1", 2]

```

- 优化：字母的大小写视为一致，比如'a'和'A'，保留一个就可以了

```js
var array3 = [1, 1, 'a', 'A', 2, 2];

// 第二版
// iteratee 英文释义：迭代 重复
/*
array：表示要去重的数组，必填
isSorted：表示函数传入的数组是否已排过序，如果为 true，将会采用更快的方法进行去重
iteratee：传入一个函数，可以对每个元素进行重新的计算，然后根据处理的结果进行去重
*/
function unique(array, isSorted, iteratee) {
    var res = [];
    var seen = [];

    for (var i = 0, len = array.length; i < len; i++) {
        var value = array[i];
        var computed = iteratee ? iteratee(value, i, array) : value;
        if (isSorted) {
            if (!i || seen !== value) {
                res.push(value)
            }
            seen = value;
        }
        else if (iteratee) {
            if (seen.indexOf(computed) === -1) {
                seen.push(computed);
                res.push(value);
            }
        }
        else if (res.indexOf(value) === -1) {
            res.push(value);
        }        
    }
    return res;
}

console.log(unique(array3, false, function(item){
    return typeof item == 'string' ? item.toLowerCase() : item
})); // [1, "a", 2]

```

## 4. Object键值对：
- 使用 typeof item + item 拼成字符串作为 key 值来避免对象的键值只能是字符串

```js
var array = [1, 2, 1, 1, '1'];

function unique(array) {
    var obj = {};
    return array.filter(function(item, index, array){
        return obj.hasOwnProperty(typeof item + item) ? false : (obj[typeof item + item] = true)
    })
}

console.log(unique(array)); // [1, 2, "1"]

```

## 5. ES6方法：

- Set

```js
ar array = [1, 2, 1, 1, '1'];

function unique(array) {
   return Array.from(new Set(array));
}

console.log(unique(array)); // [1, 2, "1"]

// 简化：
function unique(array) {
    return [...new Set(array)];
}

var unique = (a) => [...new Set(a)]
```

- Map

```js
function unique (arr) {
    const seen = new Map()
    return arr.filter((a) => !seen.has(a) && seen.set(a, 1))
}
```

## 6. 特殊类型比较：

```js
var str1 = '1';
var str2 = new String('1');

console.log(str1 == str2); // true
console.log(str1 === str2); // false

console.log(null == null); // true
console.log(null === null); // true

console.log(undefined == undefined); // true
console.log(undefined === undefined); // true

console.log(NaN == NaN); // false
console.log(NaN === NaN); // false

console.log(/a/ == /a/); // false
console.log(/a/ === /a/); // false

console.log({} == {}); // false
console.log({} === {}); // false
```

## 方法比较：
- var array = [1, 1, '1', '1', null, null, undefined, undefined, new String('1'), new String('1'), /a/, /a/, NaN, NaN];

方法|结果|说明
--- | --- | ---
for循环|[1, "1", null, undefined, String, String, /a/, /a/, NaN, NaN]|对象和 NaN 不去重
indexOf|[1, "1", null, undefined, String, String, /a/, /a/, NaN, NaN]|对象和 NaN 不去重
sort|[/a/, /a/, "1", 1, String, 1, String, NaN, NaN, null, undefined]|对象和 NaN 不去重 数字 1 也不去重
filter + indexOf|  [1, "1", null, undefined, String, String, /a/, /a/]|对象不去重 NaN 会被忽略掉
filter + sort|[/a/, /a/, "1", 1, String, 1, String, NaN, NaN, null, undefined]|对象和 NaN 不去重 数字 1 不去重
优化后的键值对方法|[1, "1", null, undefined, String, /a/, NaN]|全部去重
Set|[1, "1", null, undefined, String, String, /a/, /a/, NaN]|对象不去重 NaN 去重



# 三. 数组循环

原生js有两种方法都可以使用

- for(var i;i<arr.length;i++){}

- for(var i in arr){}

jquery有两个函数共计四种方法都可以使用

- $.each(arr,function(i,item){}),

- $(arr).each(function(i,item){}),

- $.map(arr,function(i,item){}),

- $(arr).map(function(i,item){})]

## 数组中如何跳出循环

- 1、for循环中我们使用continue；终止本次循环计入下一个循环，使用break终止整个循环。 (return)?

- 2、而在jquery中 $.each使用return true 终止本次循环计入下一个循环，return false终止整个循环。  函数返回值跟此处无关

## 1. Array.forEach()

遍历数组里的每个元素，你可以在回调函数里对每个元素进行操作。循环遍历数组中的每一项,只能遍历数组

写法：

```js
数组对象.forEach(function(参数变量名1,参数变量名2，参数变量名3)){
// 做一些操作,forEach是没有返回值,返回值为undefined
})
```

- 变量参数名1表示的是数组中的项值(数组当前项的值)

- 变量参数名2表示的是索引(数组当前项的索引)

- 变量参数名3表示原数组(数组对象本身)

1. .forEach()方法没有返回值，你不需要在回调函数里写 return

```js
var animals = ['cat','dog','mouse'];
animals.forEach(function(item){
    console.log(item);
})
```

2. 在循环中的操作对原始数组不会有影响

> 返回值:undefined,并且总是返回undefined值,并且不可链式调用

## 2. Array.map()

.map()方法能够遍历数组，再返回一个新数组，这个新数组里的元素是经过了指定的回调函数处理过的。循环遍历数组中的每一项,也只能遍历数组。

写法：

```js
数组对象.map(callback(参数名1,参数名2,参数名3){
// 对原数组做一些操作
}
```

1. 必须要有返回值,如果不给return,它会返回一个undefined

```js
var numbers = [2,3,4,5,6,7,8];

var doubleNumbers = numbers.map(function(item){
    return item*2;
});

console.log(doubleNumbers);
```

2. return 的返回值是什么,相当于给这个新增的数组添加新的值,但它不会影响原数组,只是将原来的数组拷贝了一份,把拷贝的数组项进行更改,支持链式调用

3. 如果你想修改数组里的每个元素，然后将修改后的数组存入新的数组，那使用 .map() 方法最方便。

> return 的返回值是什么,相当于给这个新增的数组添加新的值,但它不会影响原数组,只是将原来的数组拷贝了一份,把拷贝的数组项进行更改,支持链式调用

## 3. Array.filter()

.filter()方法能够 过滤掉数组中的某些元素，你可以在回调函数里设定条件，不符合条件的元素都会排除在外。

经过filter函数后会创建一个新的数组, 回调函数返回的结果一个boolean值,若结果为真,则返回匹配的项,若为假,则返回一个空数组，它不会改变原有数组,返回的是过滤后的新数组

写法：

```js
数组对象.filter(function(currentVal,index,arrs){
// 做一些操作
}
```

```js
var scores = [3,5,7,8,6,12,34,2,52];
var topScore = scores.filter(function(item){
    if(item>10){
        return true;
    }else {
        return false;
    }
})
console.log('topScore',topsore);
```

> 特点：

1. filter函数遍历的元素范围,在第一次调用回调函数callback的时候就已经确定了的

2. 在调用filter之后添加到数组中的元素不会被filter遍历到,如果已经存在的元素被改变了，则他们传入callback的值是filter遍历到他们那一刻的值,被删除或从来未被赋值的元素不会被遍历到,支持链式调用

## 4. Array.every()

.every()方法的作用是用指定的回调函数去检查数组中的每个元素，如果对于每个元素，这个回调函数都返回true，则.every()返回true。否则，.every()返回false。

```js
var ages = [23,19,45,12];
var oldersThan18 = ages.every(function(item){
    return item>18;
    
})
console.log(oldersThan18);
```

- 如果你想知道数组中的所有元素都是否符合某种条件，使用 .every() 最方便。

## 5. Array.some()

some判断是否有一个元素在判断函数中返回true。如果某个元素判断为true，则不再继续判断返回true；

```js
var array = [1,2,3,4];
console.log(array.some(function(x){return x<3}));//true
```

## 6. Array.reduce()

reduce是聚合操作，将每一个元素按照传入的函数操作，生成最终的结果。reduce的传入函数可以获得四个参数，前一个元素，当前元素，当前元素索引，数组。

```js
var array =[1,2,3,4];
var result= array.reduce(
    function(pre,current,index,array){
        return pre+current;
    }
);
console.log(result);//10
```

## 7. Array.contract()

连接两个数组

## 8. Array.find()

用来查找目标元素,若找到就返回该元素，若找不到就返回undefined，同样不会改变原有数组

写法：

```js
数组.find(callback(参数1,参数2,参数3)
```
特点:

- 找到第一个符合条件之后,就不会往后找了,这与filter过滤是不一样的，find方法比较快速便捷

- 返回值:若匿名回调函数结果为真,则返回所匹配的选项对象,若为假,则返回undefined


## 性能比较

**性能上**:for循环>forEach>map

**可读性**: forEach/map>for循环

<font color=FF0000>
区别: for循环是按顺序遍历，按照下标索引的方式进行读取访问元素的,随机访问,而forEach/map等是使用<font color=FF0000>iterator</font>迭代器进行遍历，先取到数组中的每一项的地止放入到队列中,然后按顺序取出队里的地址来访问元素

大体上讲,如果数据量不是很大的情况下,抛开业务场景和使用便利性，单纯谈性能和效率是没有意义的,一些Es5,ES6新增的数组迭代器方法方便了前端开发，使得以往复杂或者冗长的代码，可以变得易读而且精炼

好的for循环写法，在大数据量的情况下，确实也有着更好的兼容和多环境运行表现

# 四. 数组的深浅拷贝
- 浅拷贝:直接赋值的方式,简单的将它赋予其他变量，那么我们只要更改其中的任何一个，然后其他的也会跟着改变。

```js
var arr = ["One","Two","Three"];

var arrto = arr;
arrto[1] = "test";
document.writeln("数组的原始值：" + arr + "<br />");//Export:数组的原始值：One,test,Three
document.writeln("数组的新值：" + arrto + "<br />");//Export:数组的新值：One,test,Three

```

- 深拷贝
1. 方法一：js的slice函数

```js
/*对于array对象的slice函数，
返回一个数组的一段。（仍为数组）
arrayObj.slice(start, [end])
参数
arrayObj
必选项。一个 Array 对象。
start
必选项。arrayObj 中所指定的部分的开始元素是从零开始计算的下标。
end
可选项。arrayObj 中所指定的部分的结束元素是从零开始计算的下标。
说明
slice 方法返回一个 Array 对象，其中包含了 arrayObj 的指定部分。
slice 方法一直复制到 end 所指定的元素，但是不包括该元素。如果 start 为负，将它作为 length + start处理，此处 length 为数组的长度。如果 end 为负，就将它作为 length + end 处理，此处 length 为数组的长度。如果省略 end ，那么 slice 方法将一直复制到 arrayObj 的结尾。如果 end 出现在 start 之前，不复制任何元素到新数组中。*/

var arr = ["One","Two","Three"];

var arrtoo = arr.slice(0);
arrtoo[1] = "set Map";
document.writeln("数组的原始值：" + arr + "<br />");//Export:数组的原始值：One,Two,Three
document.writeln("数组的新值：" + arrtoo + "<br />");//Export:数组的新值：One,set Map,Three

```

2. 方法二：js的concat方法 

```js
/*concat() 方法用于连接两个或多个数组。
该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。
语法
arrayObject.concat(arrayX,arrayX,......,arrayX)
说明
返回一个新的数组。该数组是通过把所有 arrayX 参数添加到 arrayObject 中生成的。如果要进行 concat() 操作的参数是数组，那么添加的是数组中的元素，而不是数组。*/

var arr = ["One","Two","Three"];

var arrtooo = arr.concat();
arrtooo[1] = "set Map To";
document.writeln("数组的原始值：" + arr + "<br />");//Export:数组的原始值：One,Two,Three
document.writeln("数组的新值：" + arrtooo + "<br />");//Export:数组的新值：One,set Map To,Three
```

# 五. 分割指定长度的元素数组

```js
const listChunk = (list, size = 1, cacheList = []) => {
    const tmp = [...list]
    if (size <= 0) {
        return cacheList
    }
    while (tmp.length) {
        cacheList.push(tmp.splice(0, size))
    }
    return cacheList
}

console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9])) // [[1], [2], [3], [4], [5], [6], [7], [8], [9]]
console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9], 3)) // [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9], 0)) // []
console.log(listChunk([1, 2, 3, 4, 5, 6, 7, 8, 9], -1)) // []
```

# 六. 获取数组交集

```js
const intersection = (list, ...args) => list.filter(item => args.every(list => list.includes(item)))
const intersection = (list, arr) => list.filter(item => arr.includes(item)); // 简化
console.log(intersection([2, 1], [2, 3])) // [2]
console.log(intersection([1, 2], [3, 4])) // []
```

