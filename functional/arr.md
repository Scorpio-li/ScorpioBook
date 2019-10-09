## 1. 数组降维

1. 二维数组

```js
let arr = [ [1], [2], [3] ]
arr = Array.prototype.concat.apply([], arr); // [1, 2, 3]
```

2. 多维数组

```js
// ES6方法
let arr = [1, 2, [3], [[4]]]
arr = arr.flat(3) // [1, 2, 3, 4]
// 本地封装
function localFlat(arr){
    return arr.reduce((acc, val) => acc.concat(val),[]);
}
```

## 2. 获取数组极值

```js
function smallest(array){                           
  return Math.min.apply(Math, array);             
}                                                 
function largest(array){                            
  return Math.max.apply(Math, array);             
}  
smallest([0, 1, 2.2, 3.3]); // 0
largest([0, 1, 2.2, 3.3]); // 3.3

// ES6
let list = [1, 2, 3, 4, 5]
Math.max(...list) // 5
Math.min(...list) // 1
```



