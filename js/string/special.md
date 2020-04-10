# String(字符串)相关方法

## 空格删除

### 1. 字符串前面空格去除与替换

```js
const trimStart = str => str.replace(new RegExp('^([\\s]*)(.*)$'), '$2')
console.log(trimStart(' abc ')) // abc  
console.log(trimStart('123 ')) // 123  
```

### 2. 字符串后面空格去除与替换

```js
const trimEnd = str => str.replace(new RegExp('^(.*?)([\\s]*)$'), '$1')
console.log(trimEnd(' abc ')) //   abc  
console.log(trimEnd('123 ')) // 123  
```