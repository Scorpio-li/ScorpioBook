## 1. 判断当前网络

### 1. navigator.onLine

- 通过navigator.onLine判断当前网络状态：
```js
if(navigator.onLine){
  ...
}else{
  ...
}
```

- 非常简单，但是并不准确-根据MDN的描述：navigator.onLine只会在机器未连接到局域网或路由器时返回false，其他情况下均返回true。也就是说，机器连接上路由器后，即使这个路由器没联通网络，navigator.onLine仍然返回true。


### 2. ajax请求

- 采用get请求的方式，根据返回值判断是否能够成功get到数据，从而确定当前的网络状态：
```js
$.ajax({
  url: 'x.html',
  success: function(result){
    ...
  }, 
  error: function(result){
    ...
  }
});
```

- 这种方式的缺点在于，无法很好的区分是服务器出现故障还是用户的网络有问题。

### 3. 获取网络资源

- 原理同2，在页面放一张隐藏图片，设置其onerror函数(获取图片资源失败时会调用该函数)：
```js
<script src="./jquery-3.1.1.min.js"></script>
<script>
function getImgError(){
  alert("Network disconnect!");
}
$().ready(function(){
  $("#btn-test").click(function(){
    var imgPath = "https://www.baidu.com/img/bd_logo1.png";
    var timeStamp = Date.parse(new Date());
    $("#img-test").attr("src", imgPath + "?timestamp=" + timeStamp);
  });
});
</script>
<body>
  <img id="img-test" style="display:none;" onerror="getImgError()"/>
  <button id="btn-test">check status</button>
</body>
```

- 每次点击button时，更新该图片的src。若获取图片失败，则认为网络连接失败。
但是，这种方式的成功与否取决于保存图片的服务器是否稳定。当保存图片的服务器出现故障时，也会错误的认为是用户的网络有问题。

### 4. window.addEventListener()

- 根据MDN中的描述，可以为系统增加网络状态监听函数：

```js
window.addEventListener('online',  updateOnlineStatus);
window.addEventListener('offline', updateOnlineStatus);

// 例：

window.addEventListener('online',  function(){
  alert("onLine");
});
window.addEventListener('offline', function(){
  alert("offLine");
});
```

- 当网络状态发生变化时，浏览器通过以上监听函数可捕获到网络的状态。
该方法在下Chrome(59.0.3071.115)/Firefox(54.0.1)/IE Edge中均测试通过。














