# JavaScript之计时器

## 种类

- Promises

- setTimeout

- setInterval

- setImmediate

- requestAnimationFrame

- requestIdleCallback

### Promises 和 microtasks

一个 Promise 回调也被称为 “microtask”，它以与 MutationObserver 回调相同的频率运行。如果 queueMicrotask() 没有被规范排除并且进入浏览器领域，它也会有同样的结果。

- Promise 有一个很容易被误解的地方是它们不会给浏览器留空闲的时间。那是因为处于异步回调队列中，但是并不意味着浏览器可以进行渲染，或者处理输入，或者做其他我们希望浏览器做的工作。

```js
function block() {
  var start = Date.now()
  while (Date.now() - start < 1000) { /* wheee */ }
}
```

- 如果我们用一组 microtasks 来调用这个函数：

```js
for (var i = 0; i < 100; i++) {
  Promise.resolve().then(block)
}

// 相当于
for (var i = 0; i < 100; i++) {
  block()
}
```

- 任何同步任务执行完成后，microtasks 会立即执行。在这两者之间没有空闲做其他工作。所以，如果想把一个运行时间较长的任务分解为 microtasks，是不会如你所愿的。


### setTimeout 和 setInterval

它们是两兄弟：<font color=FF0000>setTimeout</font> 将任务排在 X 毫秒之后运行，而 <font color=FF0000>setInterval</font> 每隔 X 毫秒运行一次任务。

- 宽泛地说，setTimeout(0) 不是真正的在0毫秒之后执行。通常会在4毫秒内执行。有时会在16毫秒内执行（当 Edge 在充电时会这样）。这些是浏览器必须具备的能力，为了防止不受控制的网页占用 CPU 执行无用的 setTimeout。

- setTimeout 确实允许浏览器在回调函数被调用之前做一些工作（和 microtasks 不同）。但是，如果你想在回调之前进行输入或是渲染操作，一般来说 setTimeout 不是最好的选择，因为它只是偶尔允许在回调之前做其他操作。 

### setImmediate

setImmediate 只被 IE 和 Edge 采用了。仍在使用的部分原因是它在 IE 浏览器中作用很大，它允许输入事件比如键盘输入和鼠标点击“跳过队列”并在 setImmediate 回调之前执行，而 setTimeout 在 IE 中就没有这么大魔力。（


### requestAnimationFrame

有一个最重要的 setTimeout 替代品，一个真正挂在浏览器渲染循环中的定时器。

- requestAnimationFrame 基本上是这样工作的：它虽然和 setTimeout 有点像，但是它会在浏览器下次重绘时调用，而非等待一些无法预测的时间（4毫秒，16毫秒，1秒等）。

- requestAnimationFrame 的使用方式是这样的：无论什么时候，只要我知道我将要修改浏览器的样式或布局——举个例子，改变 CSS 属性或启动一个动画——我就会把它放在 requestAnimationFrame（这里缩写为 rAF）。

    1. 我不太可能打乱布局，因为所有的DOM的变化都在排队和协调。
    
    2. 我的代码会自然地去适应浏览器的性能特点。举个例子，如果这里有一个配置较低的设备正在试图渲染一些DOM元素，rAF 会自然地从通常的16.7毫秒（在60赫兹的屏幕上）时间间隔慢下来，因此，它不会像运行了大量 setTimeout 或 setInterval 的一样让设备崩溃。

### requestIdleCallback

