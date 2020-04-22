# console 命令

## console.log()

经典的 <font color=FF0000>console.log</font> 其实有着丰富的函数特性。尽管大多数人只使用 console.log(object) 这种语法，但你仍然能写 <font color=FF0000>console.log(object, otherObject, string)</font> 并且它会将所有东西都整齐的打印出来。有时候确实很方便。

```js
console.log('I like %s but I do not like %s.', 'Skittles', 'pus');
// 输出
// > I like Skittles but I do not like pus.
```

- 一般的占位符有 %o（这是字符 o，不是 0）表示一个对象，%s 表示一个字符串，以及 %d 代表一个小数或者整数。

- 另一个有趣是 %c。实际上它是作为 CSS 值的占位符。

```js
console.log('I am a %cbutton%c', 'color: white; background-color: orange; padding: 2px 5px; border-radius: 2px');
```

## console.dir()

通常来看，console.dir() 功能和 log() 非常相似，尽管看起来有略微不同。

- 下拉小箭头展示的对象信息和 console.log 的视图里一样。但是在你观察元素节点的时候，两者结果会非常有趣并且截然不同。

- console.dir()是一种更对象化的方式去观察元素节点。

## console.warn()

- 可能是 log() 最直接明显的替换，你可以用相同的方式使用 console.warn()。唯一的区别在于输出是一抹黄色。

- 还有一个更大的优点。因为输出是一个 warn 级别而不是一个 info 级别，你可以将所有的 console.log 过滤掉只留下 console.warn。

## console.table()

console.table() 方法更偏向于一种方式展示列表形式的数据，这比只扔下原始的对象数组要更加整洁。

```js
const transactions = [{
  id: "7cb1-e041b126-f3b8",
  seller: "WAL0412",
  buyer: "WAL3023",
  price: 203450,
  time: 1539688433
},
{
  id: "1d4c-31f8f14b-1571",
  seller: "WAL0452",
  buyer: "WAL3023",
  price: 348299,
  time: 1539688433
},
{
  id: "b12c-b3adf58f-809f",
  seller: "WAL0012",
  buyer: "WAL2025",
  price: 59240,
  time: 1539688433
}];
```

![console.table(data) 的输出](/resource/image/js/console-table.png)

- 第二个可选参数是你想要显示列表的某列。默认是整个列表，但是我们也能这样做。

```js
> console.table(data, ["id", "price"]);
```

- 值得一提的是在最右一列头部的右上角有个箭头可以颠倒次序。点击了它，会排序整个列。非常方便的找出一列的最大或者最小值，或者只是得到不同的数据展示形式。

- console.table() 只有处理最多1000行的数据的能力，所以它可能并不适用于所有的数据集合。

## console.assert()

一个经常被忽视的实用的函数，assert() 在第一个参数是 falsey 时和 log() 一样。当第一个参数为真值时也什么都不做。

- 这个在你需要循环（或者不同的函数调用）并且只有一个要显示特殊的行为的场景下特别有用。本质上和这个是一样的。

```js
if (object.whatever === 'value') {
  console.log(object);
}
```

## console.count()

```js
for(let i = 0; i < 10000; i++) {
  if(i % 2) {
    console.count('odds');
  }
  if(!(i % 5)) {
    console.count('multiplesOfFive');
  }
  if(isPrime(i)) {
    console.count('prime');
  }
}

// 运行结果
odds: 1
odds: 2
prime: 1
odds: 3
multiplesOfFive: 1
prime: 2
odds: 4
prime: 3
odds: 5
multiplesOfFive: 2
...
```

- console.count()，不需要参数。使用 default 调用。

- console.countReset()，如果你希望重置计数器可以使用它。

## console.trace()

- 在你试图找出有问题的内部类或者库的调用这一块是它最擅长。

```js
export default class CupcakeService {
    
  constructor(dataLib) {
    this.dataLib = dataLib;
    if(typeof dataLib !== 'object') {
      console.log(dataLib);
      console.trace();
    }
  }
  ...
}
// 这里单独使用 console.log() 我们只能知道执行了哪一个基础库，并不知道执行的具体位置。但是，堆栈轨迹会清楚的告诉我们问题在于 Dashboard.js，我们从中发现 new CupcakeService(false) 是造成出错的罪魁祸首。
```

## console.time()

console.time() 是专门用于监测操作的时间开销的函数，也是监测 JavaScript 细微时间的更好的方式。

```js
function slowFunction(number) {
  var functionTimerStart = new Date().getTime();
  // something slow or complex with the numbers. 
  // Factorials, or whatever.
  var functionTime = new Date().getTime() - functionTimerStart;
  console.log(`Function time: ${ functionTime }`);
}
var start = new Date().getTime();

for (i = 0; i < 100000; ++i) {
  slowFunction(i);
}

var time = new Date().getTime() - start;
console.log(`Execution time: ${ time }`);
```

- 这是一个过时的方法。我指的同样还有上面的 console.log。大多数人没有意识到这里你本可以使用模版字符串和插值法。它时不时的会帮助到你。

```js
const slowFunction = number =>  {
  console.time('slowFunction');
  // something slow or complex with the numbers. 
  // Factorials, or whatever.
  console.timeEnd('slowFunction');
}
console.time();

for (i = 0; i < 100000; ++i) {
  slowFunction(i);
}
console.timeEnd();
```

## console.group()

如今我们可能在大多数 console 中要输出高级和复杂的东西。分组可以让你归纳这些。尤其是让你能使用嵌套。它擅长展示代码中存在的结构关系。

```js
// this is the global scope
let number = 1;
console.group('OutsideLoop');
console.log(number);
console.group('Loop');
for (let i = 0; i < 5; i++) {
  number = i + number;
  console.log(number);
}
console.groupEnd();
console.log(number);
console.groupEnd();
console.log('All done now');
```

- console.groupCollapsed。功能上和 console.group 一样，但是分组块一开始是折叠的。