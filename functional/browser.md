# URL

## 1. parseQueryString(url参数转对象)

```js
/**
 * 
 * @desc   url参数转对象
 * @param  {String} url  default: window.location.href
 * @return {Object} 
 */
function parseQueryString(url) {
    url = url == null ? window.location.href : url
    var search = url.substring(url.lastIndexOf('?') + 1)
    if (!search) {
        return {}
    }
    return JSON.parse('{"' + decodeURIComponent(search).replace(/"/g, '\\"').replace(/&/g, '","').replace(/=/g, '":"') + '"}')
}
```

## 2. stringfyQueryString(对象序列化)
```js
/**
 * 
 * @desc   对象序列化
 * @param  {Object} obj 
 * @return {String}
 */
function stringfyQueryString(obj) {
    if (!obj) return '';
    var pairs = [];
    for (var key in obj) {
        var value = obj[key];
        if (value instanceof Array) {
            for (var i = 0; i < value.length; ++i) {
                pairs.push(encodeURIComponent(key + '[' + i + ']') + '=' + encodeURIComponent(value[i]));
            }
            continue;
        }
        pairs.push(encodeURIComponent(key) + '=' + encodeURIComponent(obj[key]));
    }
    return pairs.join('&');
}
```

## 3. 利用 a 标签解析 URL
```js
/*
 @url 标签路径
*/
function parseURL(url) {
    var a =  document.createElement('a');
    a.href = url;
    return {
        host: a.hostname,
        port: a.port,
        query: a.search,
        params: (function(){
            var ret = {},
                seg = a.search.replace(/^\?/,'').split('&'),
                len = seg.length, i = 0, s;
            for (;i<len;i++) {
                if (!seg[i]) { continue; }
                s = seg[i].split('=');
                ret[s[0]] = s[1];
            }
            return ret;
        })(),
        hash: a.hash.replace('#','')
    };
}
```

## 4. 获取URL中的参数

- 简单版: 不兼容ie

```js
var urlParams = new URLSearchParams('?post=1234&action=edit');
console.log(urlParams.get('action')); // "edit"
```

- 复杂版：

```js
function getUrlParams(param){
  // 有赖于浏览器环境， window.location.search 是浏览器函数
  // 意思是:设置或返回从问号 (?) 开始的 URL（查询部分）。       
  var query = window.location.search.substring(1);       
  var vars = query.split("&");       
  for (var i=0;i<vars.length;i++) {               
    var pair = vars[i].split("=");               
    if(pair[0] == param){return pair[1];}       
  }       
  return(false);
}
```


# Browser Type

## 1. 手机端判断浏览器类型

- 目前主要支持 安卓 & 苹果 & ipad & 微信 & 支付宝 & 是否是手机端。

```js
BrowserInfo = {      
  isAndroid: Boolean(navigator.userAgent.match(/android/ig)),      
  isIphone: Boolean(navigator.userAgent.match(/iphone|ipod/ig)),      
  isIpad: Boolean(navigator.userAgent.match(/ipad/ig)),      
  isWeixin: Boolean(navigator.userAgent.match(/MicroMessenger/ig)),      
  isAli: Boolean(navigator.userAgent.match(/AlipayClient/ig)),
  isPhone: Boolean(/(iPhone|iPad|iPod|iOS|Android)/i.test(navigator.userAgent))
}
```





