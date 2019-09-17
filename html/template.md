# HTML5页面开发的基础模板

## 标准模板

```html
<!-- 让浏览器使用html5的标准解析 -->
<!doctype html>
<html>
    <head> 
        <!-- 设置字符编码集让浏览器使用utf8解析当前网页 --> 
        <meta http-equiv="Content-Type" content="text/html; charset=utf8" />
        <meta name="keywords" content="SEO搜索引擎，关键词，多个请用逗号分开" /> 
        <meta name="description" content="网页描述，八十字内" />
        <title>浏览器标签页上的网页标题</title>
     </head> 
<body> 
<!-- 所有的标签学习都在这body里面去敲，上面head元素里面的内容做个了解就可以了 -->  
<h1>我是大标题</h1> <h2>我是主题2</h2> 
<h3>我是主题3</h3> <h4>我是主题4</h4> 
<h5>我是主题5</h5> <h6>我是主题6</h6>  
</body>
</html>
```
<!-- more -->

## 开发版本：

```html
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta charset="utf-8">
<title></title>
<meta name="description" content="">
<meta name="author" content="">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet" href="">
<!--[if lt IE 9]>
<script src="//cdn.jsdelivr.net/html5shiv/3.7.2/html5shiv.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->
<link rel="shortcut icon" href="">
</head>
<body>
 
<!-- 这里添加页面主要内容 -->
 
<!-- SCRIPTS：个人建议在天朝不要使用Google的CDN了，是不是你就发现你的网站功能失效了 -->
<!-- Example: <script src="//ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script> -->
</body>
</html>
```

## 注释版本

```html
<!DOCTYPE html>
<!-- 
     设置lang值来保证<html>标签的互操作性及其可访问性
　  更多HTML标签全局性属性
　  请阅读这里: http://www.w3.org/TR/html-markup/global-attributes.html -->
<html>
 
<head>
 
<!--
    告诉IE使用目前最新的布局引擎：
   &nbsp;更多信息阅读这里: https://www.modern.ie/en-us/performance/how-to-use-x-ua-compatible -->
<meta http-equiv="X-UA-Compatible" content="IE=edge">
 
<!--
     针对web性能定义字符集，首选通过HTTP header来设置
　  确保HTTP header和Meta标签设置一致
　  更多信息阅读这里: https://developers.google.com/speed/docs/best-practices/rendering#SpecifyCharsetEarly -->
<meta charset="utf-8"> 
 
<!-- 指定页面标题 -->
<title></title>
 
<!-- 指定web页面描述 -->
<meta name="description" content="">
 
<!-- 指定web页面作者 -->
<meta name="author" content="">
 
<!-- 提示移动浏览器使用设备宽度和缩放比 -->
<meta name="viewport" content="width=device-width, initial-scale=1">
 
<!-- 在页面加载前来加载CSS
     保证相关样式的及时加载
     指定对应的URI属性 -->
<link rel="stylesheet" href="">
 
<!--
     加载htmlshiv和respond.js来兼容老版本的IE浏览器
　  方便使用HTML5中的新元素和media queries -->
<!--[if lt IE 9]>
<script src="//cdn.jsdelivr.net/html5shiv/3.7.2/html5shiv.min.js"></script>
<script src="//cdnjs.cloudflare.com/ajax/libs/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->
 
<!-- 指定favicon的URI -->
<link rel="shortcut icon" href="">
 
<!-- 下面注释掉的是ios/android书签图标-->
<!--
<meta name="mobile-web-app-capable" content="yes">
<link rel="icon" sizes="196x196" href="">
<link rel="apple-touch-icon" sizes="152x152" href="">
-->
 
<!-- 
     如果可能使用async属性来非阻断的加载脚本
　  例子: <script src="" async></script> -->
</head>
<body>
 
<!-- 这里添加页面主要内容 -->
 
<!-- 如果可能使用async属性来非阻断的加载脚本 -->
<!-- SCRIPTS -->
<!-- 例子: <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script> -->
</body>
</html>
```