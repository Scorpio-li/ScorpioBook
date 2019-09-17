## 1.命令：初始化项目
- express #在当前目录下创建express框架，默认使用jade引擎

- express -e #在当前目录下创建express框架，默认使用ejs引擎

- express project#在project目录下创建express框架，默认使用jade引擎 

- express -e project#在project目录下创建express框架，默认使用ejs引擎 

- express --version #显示当前版本

- express -h，查看所有的帮助信息

```s
npm install -g express-generator
# 初始化项目
express projectName
# 安装依赖
npm install
# 启动服务器
npm start
```
<!-- more -->
## 2.express目录框架：

```s
│ app.js #主要的入口文件，或者说起始文件
│ package.json #模块配置文件
│
├─bin #启动脚本
   │ www #启动文件:命令为 node www 
├─node_modules #依赖的模块
│ 
├─public #一些静态文件，如图片、JS、CSS 件
│ ├─images
│ ├─javascripts
│ └─stylesheets
│ style.css 
│

├─routes #路由文件，目前express 支持将一个虚拟目录下的请求放到要给路由 件中，这是在app.js中定义的

│ index.js  #app.use('/',routes) ->根目录下的路由
│ users.js  #app.use('/user',routes) ->user目录下的路由
│
└─views     #mvc的view层，模板文件存放的目录
error.ejs
index.ejs
```
- 默认的路由文件index.js如下:

```js
var express = require('express');
var router = express.Router();
/* GET home page. */
router.get('/', function(req, res) {
res.render('index', { title: 'Express' });
});
module.exports = router;
```
这里只有一个针对根目录的路由，是以get方式访问的，对 应的函数有两个参数，req和res，分为为输入对象和输出对象。

## 3.express核心概念：
- 中间件：可以毫不夸张的说，在express应用中，一切皆中间件。各种应用逻辑，如cookie解析、会话处理、日志记录、权限校验等，都是通过中间件来完成的。
![image](https://user-gold-cdn.xitu.io/2017/4/28/28d4ba428b9537b7e0b936c48268d685.png?imageView2/0/w/1280/h/960/ignore-error/1)     
    1. 参数：三个参数，熟悉http.createServer()的同学应该比较眼熟，其实就是req（客户端请求实例）、res（服务端返回实例），只不过进行了扩展，添加了一些使用方法。
    2. next：回调方法，当next()被调用时，就进入下一个中间件。
    
    ```js
    var express = require('express');
    var app = express();
    
    app.use(function(req, res, next) {
        console.log('1');
        next();
    });
    
    app.use(function(req, res, next) {
        console.log('2');
        next();
    });
    
    app.use(function(req, res, next) {
        console.log('3');
        res.send('hello');
    });
    
    app.listen(3000);

    ```

- 中间件分类：
    1. 应用级中间件：app.use()、app.METHODS()接口中使用的中间件。
    2. 路由级中间件：router.use()、router.METHODS()接口中使用的中间件。
    
        ```js
        var express = require('express');
        var app = express();
        var user = express.Router();
        
        // 应用级
        app.use(function(req, res, next){
            console.log('收到请求，地址为：' + req.url);
            next();
        });
        
        // 应用级
        app.get('/profile', function(req, res, next){
            res.send('profile');
        });
        
        // 路由级
        user.use('/list', function(req, res, next){
            res.send('/user/list');
        });
        
        // 路由级
        user.get('/detail', function(req, res, next){
            res.send('/user/detail');
        });
        
        app.use('/user', user);
        
        app.listen(3000);
        ```
- 路由：地球人都知道，负责寻址的。比如用户发送了个http请求，该定位到哪个资源，就是路由说了算。
    1. 路由分类：
        ```js
        var express = require('express');
        var app = express();
        
        // 1.路由：字符串类型
        app.get('/book', function(req, res, next){
            res.send('book');
        });
        
        // 2.路由：字符串模式
        app.get('/user/*man', function(req, res, next){
            res.send('user');  // 比如： /user/man, /user/woman
        });
        
        // 3.路由：正则表达式
        app.get(/animals?$/, function(req, res, next){
            res.send('animal');  // 比如： /animal, /animals
        });
        
        // 4.路由：命名参数
        app.get('/employee/:uid/:age', function(req, res, next){
            res.json(req.params);  // 比如：/111/30，返回 {"uid": 111, "age": 30}
        });
        
        app.listen(3000);
        
        ```
    2. 路由拆分：通过express.Router()进行了路由拆分
        ```js
        <!--路由拆分前-->
        var express = require('express');
        var app = express();
        
        app.get('/user/list', function(req, res, next){
            res.send('/list');
        });
        
        app.get('/user/detail', function(req, res, next){
            res.send('/detail');
        });
        
        app.listen(3000);
        
        <!--路由拆分后-->
        var express = require('express');
        var app = express();
        
        var user = express.Router();
        
        user.get('/list', function(req, res, next){
            res.send('/list');
        });
        
        user.get('/detail', function(req, res, next){
            res.send('/detail');
        });
        
        app.use('/user', user); // mini app，通常做应用拆分
        
        app.listen(3000);
        
        ```
- 模板引擎：负责视图动态渲染。下面会介绍相关配置，以及如何开发自己的模板引擎。
    ```js
    // view engine setup
    app.set('views', path.join(__dirname, 'views'));
    app.set('view engine', 'jade');
    ```
    1.配置：
    ```js
    views：模版文件放在哪里，默认是在项目根目录下。举个例子：app.set('views', './views')
    view engine：使用什么模版引擎，举例：app.set('view engine', 'jade')
    ```
## 4.api
- req

```js
req.params.name ->/user/:name
req.query.name ->/user?name=shiyq
req.body.name ->名称为name的表单输入值
req.param(name) ->以上的三种输入都支持，次序为params,body,query req.cookie.name ->cookie的name属性
```
- res

```js
res.cookie(name,value) ->设置cookie
res.redirect('/foo/bar') ->跳转到/foo/bar
res.location('foo/bar') ->类似redirect
res.send('<p>name</p>') ->向浏览器输出
res.json() ->向浏览器返回json数据
res.render(view, [locals], callback) ->转向view，并携带变量 
res.end() ->结束输出
```