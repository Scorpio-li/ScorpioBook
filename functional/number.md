## 1. 判断数字是否相等

- 小数：用户输入的是十进制数字，计算机保存的是二进制数。所以计算结果会有偏差，所以我们不应该直接比较非整数，而是取其上限，把误差计算进去。这样一个上限称为 machine epsilon，双精度的标准 epsilon 值是 2^-53 （Math.pow(2, -53)）

```js
function epsEqu(x,y) {  
  return Math.abs(x - y) < Math.pow(2, -52);
}
// 举例
0.1 + 0.2 === 0.3 // false
epsEqu(0.1 + 0.2, 0.3) // true

// 方法2
function epsEqu(x,y) {  
  return Math.abs(x - y) < Number.EPSILON;
}
```