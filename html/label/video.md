## video标签和audio标签

- video标签和audio标签还可以出发很多事件和方法。这些方法监控着不同的属性的变化，这些变化有可能是媒体播放的结果，也可能是用户操作媒体的结果。

### 媒体元素的相关事件：

- abort：触发时机是下载中断。

- canplay：在可以播放的时候，readyState的值为2的时候触发。

- canplaythrough：readyState的值为3的时候，触发。播放可以继续，而应该不会中断的时候触发。

- canshowcurrentframe：readyState的值为1的时候，触发。当前帧已经下载完成的时候触发。

- dataunavailable：因为没有数据而不能播放的时候，readyState的值为0。

- durationchange：duration属性值改变触发的事件。

- emptied：网络连接关闭。

- empty：发生错误阻止了媒体下载。

- ended：媒体播放到末尾，播放停止(只读)

- error：下载期间发生网络错误。

- load：触发时间所有媒体已经加载完成。这个事件可能会被废弃，建议使用canplaythrough。

- loadeddata：触发时间媒体的第一帧已经加载完成。

- loadedmetadata：触发时机媒体的元素数据已经加载完成。

- loadstart：下载已经开始。

- pause：方法是媒体开始暂停。

- play：方法是媒体开始播放。

- playing：媒体已经实际开始播放。

- progress：正在下载。

- ratechange：播放媒体的速度改变。

- seeked：搜索结束。

- seeking：正移动到新位置。

- stalled：浏览器尝试下载，但未接收到数据。

- volumechange：触发时间是volume属性或muted属性值已经改变。

- waiting：触发时间是播放暂停，等待下载更多数据。