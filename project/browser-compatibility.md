# 浏览器兼容

## 1. 明确兼容的浏览器范围：
<!-[if !IE]> 除IE外都可识别 <![endif]-><br />
<!-[if IE]> 所有的IE可识别 <![endif]-><br />
<!-[if IE 6]> 仅IE6可识别 <![endif]-><br />
<!-[if lt IE 6]> IE6以及IE6以下版本可识别 <![endif]-><br />
<!-[if gte IE 6]> IE6以及IE6以上版本可识别 <![endif]-><br />
<!-[if IE 7]> 仅IE7可识别 <![endif]-><br />
<!-[if lt IE 7]> IE7以及IE7以下版本可识别 <![endif]-><br />
<!-[if gte IE 7]> IE7以及IE7以上版本可识别 <![endif]-><br />
<!-[if IE 8]> 仅IE8可识别 <![endif]-><br />
<!-[if IE 9]> 仅IE9可识别 <![endif]--><br />

## 2. 符号解释：
- ！（非）;
- lt (小于);
- lte(小于或等于);
- gt(大于);
- gte(大于或等于);
- &(与);
- |(或);

## 3. 检查页面中的伪类和伪元素，不支持的伪类和伪元素要换通用的方法兼容

## 4. 排查CSS3兼容问题

## 5. 使用CSS hack
[CSS hack大全](http://www.webhj.com/hj-650.html)

## 6.判断浏览器类型：
方式一：

```
var isIE=!!window.ActiveXObject;
var isIE6=isIE&&!window.XMLHttpRequest;
var isIE8=isIE&&!!document.documentMode;
var isIE7=isIE&&!isIE6&&!isIE8;
if (isIE){
    if (isIE6){
        alert('ie6');
    }else if (isIE8){
        alert('ie8');
    }else if (isIE7){
        alert('ie7');
    }
}
```

方式二：
```
if(navigator.appName == 'Microsoft Internet Explorer' && navigator.appVersion.match(/6./i)=='6.'){
    alert('IE 6');
}
else if(navigator.appName == 'Microsoft Internet Explorer' && navigator.appVersion.match(/7./i)=='7.'){
    alert('IE 7');
}
else if(navigator.appName == 'Microsoft Internet Explorer' && navigator.appVersion.match(/8./i)=='8.'){
    alert('IE 8');
}
else if(navigator.appName == 'Microsoft Internet Explorer' && navigator.appVersion.match(/9./i)=='9.'){
    alert('IE 9');
}
```

方式三：
```
if(navigator.userAgent.indexOf('Opera') != -1) {
alert('Opera');
}
else if(navigator.userAgent.indexOf('MSIE') != -1) {
alert('Internet Explorer');
}
else if(navigator.userAgent.indexOf('Firefox') != -1) {
alert('Firefox');
}
else if(navigator.userAgent.indexOf('Netscape') != -1) {
alert('Netscape');
}
else if(navigator.userAgent.indexOf('Safari') != -1) {
alert('Safari');
}
else{
alert('无法识别的浏览器。');
}
```