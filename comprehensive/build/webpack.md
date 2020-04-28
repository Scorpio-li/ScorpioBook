# webpack教程（Demo集合）

[阮一峰教程地址](https://github.com/ruanyf/webpack-demos)
[webpack文档](https://webpack.docschina.org/)

## 安装使用指南

1. 首先，全局安装Webpack和webpack-dev-server

```js
$ npm i -g webpack webpack-dev-server
```

2. 然后克隆clone阮一峰的仓库

```js
$ git clone https://github.com/ruanyf/webpack-demos.git
```

3. 安装依赖

```js
$ cd webpack-demos
$ npm install
```

4. 进入demo*目录并且运行它们

```js
$ cd demo01
$ npm run dev
```

上面的代码不会自动的打开你的浏览器，需要手动访问http://127.0.0.1:8080

## 前言：Webpack是什么

Webpack用于构建Javascript模块脚本来给浏览器使用的前端工具。

```js
$ browserify main.js > bundle.js
// # 上下代码作用相同
$ webpack main.js bundle.js
```

- Webpack需要一个名为<font color=FF0000>webpack.config.js</font>的配置文件，这个文件就是一个CommonJS的模块（module）

```js
// webpack.config.js的内容
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};
```

- 必须知道的参数选项如下:

    - <font color=FF0000>webpack</font>——开发时的构建命令

    - <font color=FF0000>webpack -p</font>——发布产品时的构建命令

    - <font color=FF0000>webpack --watch</font>——用于增量开发的构建

    - <font color=FF0000>webpack -d</font>——包括source maps

    - <font color=FF0000>webpack --colors</font>——让构建输出更好看


- 可以在定制webpack.config.js中的<font color=FF0000>scripts</font>选项，如下所示

```js
// package.json
{
  // ...
  "scripts": {
    "dev": "webpack-dev-server --devtool eval --progress --colors",
    "deploy": "NODE_ENV=production webpack -p"
  },
  // ...
}
```


## Demo示例

### Demo01:入口文件

入口文件用来Webpack读取它然后构建<font color=FF0000>bundle.js</font>

例如：
```js
// main.js就是一个入口文件
document.write('<h1>Hello World</h1>');
```

```html
<!-- index.html -->
<html>
  <body>
    <script type="text/javascript" src="bundle.js"></script>
  </body>
</html>
```

- Webpack依据webpack.config.js来构建bundle.js

```js
// webpack.config.js
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};
```

### Demo02:多个入口文件

Webpack允许多个入口文件存在，在多页面的app中很有用，每个页面有不同的入口文件。

```js
// main1.js
document.write('<h1>Hello World</h1>');

// main2.js
document.write('<h2>Hello Webpack</h2>');
```

```html
<!-- index.html -->
<html>
  <body>
    <script src="bundle1.js"></script>
    <script src="bundle2.js"></script>
  </body>
</html>
```

- webpack.config.js

```js
module.exports = {
  entry: {
    bundle1: './main1.js',
    bundle2: './main2.js'
  },
  output: {
    filename: '[name].js'
  }
};
```

### Demo03:Babel-loader

加载器(Loaders)是一些预处理器，用于在Webpack的构建过程前，将你app里的一些资源文件进行转换。

例如，Babel-loader能够将JSX/ES6文件转为普通的JS文件，之后Webpack能够开始构建它们。

```js
// main.jsx是一个JSX文件
// main.jsx
const React = require('react');
const ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.querySelector('#wrapper')
);
```

```html
// index.html
<html>
  <body>
    <div id="wrapper"></div>
    <script src="bundle.js"></script>
  </body>
</html>
```

```js
// webpack.config.js
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['es2015', 'react']
          }
        }
      }
    ]
  }
};
```

### Demo04:CSS-loader

Webpack允许在JS文件中包含CSS，需要CSS-loader对这些CSS进行处理

```js
// main.js
require('./app.css');
```

```css
// app.css
body {
  background-color: blue;
}
```

```html
// index.html
<html>
  <head>
    <script type="text/javascript" src="bundle.js"></script>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

```js
// webpack.config.js
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    rules:[
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      },
    ]
  }
};
```

::: tip
注意！必须使用两个加载器来转换CSS文件。CSS-loader用来读取CSS文件来转换，另一个Style-loader用来往HTML中插入 style 标签。
:::

事实上，Webpack将CSS文件的内容直接插入到index.html

```html
<head>
  <script type="text/javascript" src="bundle.js"></script>
  <style type="text/css">
    body {
      background-color: blue;
    }
  </style>
</head>
```

### Demo5: Image loader

Webpack能够将图片包含进JS文件中

```js
// main.js
var img1 = document.createElement("img");
img1.src = require("./small.png");
document.body.appendChild(img1);

var img2 = document.createElement("img");
img2.src = require("./big.png");
document.body.appendChild(img2);
```

- index.html

```html
<html>
  <body>
    <script type="text/javascript" src="bundle.js"></script>
  </body>
</html>
```

- webpack.config.js

```js
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    rules:[
      {
        test: /\.(png|jpg)$/,
        use: [
          {
            loader: 'url-loader',
            options: {
              limit: 8192
            }
          }
        ]
      }
    ]
  }
};
```

url-loader将image文件转为 img 标签，如果图片大小 < 8192字节，它将转换为Data url（翻译：图片变为Base64编码，减少请求次数），否则，他将转为普通文件URL。

```html
<img src="data:image/png;base64,iVBOR...uQmCC">
<img src="4853ca667a2b8b8844eb2693ac1b2578.png">
```

### Demo06:CSS Module

<font color=FF0000>css-loader?modules</font>（请求参数为modules）能够使用CSS Module，CSS Module带给你的JS文件模块中的CSS一个局部作用域，也可以使用<font color=FF0000>:global(selector)</font>让CSS变为全局作用。

- index.html

```html
<html>
<body>
  <h1 class="h1">Hello World</h1>
  <h2 class="h2">Hello Webpack</h2>
  <div id="example"></div>
  <script src="./bundle.js"></script>
</body>
</html>
```

- app.css

```css
/* local scope */
.h1 {
  color:red;
}

/* global scope */
:global(.h2) {
  color: blue;
}
```

- main.jsx

```js
var React = require('react');
var ReactDOM = require('react-dom');
var style = require('./app.css');

ReactDOM.render(
  <div>
    <h1 className={style.h1}>Hello World</h1>
    <h2 className="h2">Hello Webpack</h2>
  </div>,
  document.getElementById('example')
);
```

- webpack.config.js

```js
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    rules:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['es2015', 'react']
          }
        }
      },
      {
        test: /\.css$/,
        use: [
          {
            loader: 'style-loader'
          },
          {
             loader: 'css-loader',
             options: {
               modules: true
             }
          }
        ]
      }
    ]
  }
};
```

访问 http://127.0.0.1:8080 会看到只有h1是红色的，因为他的CSS是局部作用域，然后所以h2都是蓝色的，因为它是全局作用域。

### Demo07:UglifyJs Plugin

Webpack用插件系统来扩展他的功能。例如，UglifyJs Plugin，它用来压缩JS代码，使得JS文件体积变小。

- main.js

```js
var longVariableName = 'Hello';
longVariableName += ' World';
document.write('<h1>' + longVariableName + '</h1>');
```

- index.html

```html
<html>
<body>
  <script src="bundle.js"></script>
</body>
</html>
```

- webpack.config.js

```js
var webpack = require('webpack');
var UglifyJsPlugin = require('uglifyjs-webpack-plugin');

module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  plugins: [
    new UglifyJsPlugin()
  ]
};
```

在访问服务器后，可以看到main.js最小化为如下代码：

```js
var o="Hello";o+=" World",document.write("<h1>"+o+"</h1>")
```

### Demo08:HTML Webpack Plugin和Open Browser Webpack Plugin

这个demo用来展示如何加载第三方插件
<font color=FF0000>html-webpack-plugin</font>能为你创建<font color=FF0000>index.html，open-browser-webpack-plugin</font>能够在Webpack加载时打开一个新的浏览器标签(tab)

- main.js

```js
document.write('<h1>Hello World</h1>');
```

- webpack.config.js

```js
var HtmlwebpackPlugin = require('html-webpack-plugin');
var OpenBrowserPlugin = require('open-browser-webpack-plugin');

module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  plugins: [
    new HtmlwebpackPlugin({
      title: 'Webpack-demos',
      filename: 'index.html'
    }),
    new OpenBrowserPlugin({
      url: 'http://localhost:8080'
    })
  ]
};
```

现在你不用手动创建index.html也不用手动打开浏览器了。




### Demo09:环境变量(Environment flags)

使用环境变量让一些代码只能在开发环境时使用。

- main.js

```js
document.write('<h1>Hello World</h1>');

if (__DEV__) {
  document.write(new Date());
}
```

- index.html

```html
<html>
<body>
  <script src="bundle.js"></script>
</body>
</html>
```

- webpack.config.js

```js
var webpack = require('webpack');

var devFlagPlugin = new webpack.DefinePlugin({
  __DEV__: JSON.stringify(JSON.parse(process.env.DEBUG || 'false'))
});

module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  plugins: [devFlagPlugin]
};
```

现在传递环境变量给Webpack。打开<font color=FF0000>demo09/package.json</font>，找到如下scripts选项

```json
// package.json
{
  // ...
  "scripts": {
    "dev": "cross-env DEBUG=true webpack-dev-server --open",
  },
  // ...
}
```

### Demo10:代码分离

在大型web应用中，将所有代码放入一个文件是十分低效的。Webpack允许你将大型JS文件分成多块。特别的，如果一些代码块只是在某些情况下需要，那么这些代码块会按需加载。

Webpack使用<font color=FF0000>require.ensure</font>来定义一个分割点

- main.js

```js
// main.js
require.ensure(['./a'], function (require) {
  var content = require('./a');             
  document.open();
  document.write('<h1>' + content + '</h1>');
  document.close();
});
```

<font color=FF0000>require.ensure</font>告诉Webpack <font color=FF0000>./a,js</font>需要从<font color=FF0000>bundle.js</font>中分离出来作为一个单独的块文件

- a.js

```js
// a.js
module.exports = 'Hello World';
```

现在Webpack关心依赖、输出文件、运行时的东西。你不必将多余的东西放到index.html和webpack.config.js中

- index.html

```html
<html>
  <body>
    <script src="bundle.js"></script>
  </body>
</html>
```

- webpack.config.js

```js
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  }
};
```

访问服务器后，你感觉不到任何不同。实际上，**Webpack**将构建**main.js**和**a.js**到不同的块中（**bundle.js**和**0.bundle.js**），然后从**bundle.js**中按需加载**0.bundle.js**

### Demo11:bundle-loader下的代码分离

另一个代码分割的方式是bundle-loader

```js
// main.js

// Now a.js is requested, it will be bundled into another file
var load = require('bundle-loader!./a.js');

// To wait until a.js is available (and get the exports)
//  you need to async wait for it.
load(function(file) {
  document.open();
  document.write('<h1>' + file + '</h1>');
  document.close();
});
```
require('bundle-loader!./a.js')告诉Webpack从其他块加载a.js
现在main.js构建为bundle.js，a.js构建为0.bundle.js

### Demo12:通用块

在多个JS脚本中有通用块，通过<font color=FF0000>CommonsChunkPlugin</font>你能提取不同文件中的通用部分，对于浏览器缓存来节省带宽是非常有用的。

```js
// main1.jsx
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>Hello World</h1>,
  document.getElementById('a')
);

// main2.jsx
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h2>Hello Webpack</h2>,
  document.getElementById('b')
);
```

- index.html

```html
<html>
  <body>
    <div id="a"></div>
    <div id="b"></div>
    <script src="commons.js"></script>
    <script src="bundle1.js"></script>
    <script src="bundle2.js"></script>
  </body>
</html>
```

上面的commons.js是main1.jsx和main2.jsx的通用部分。正如你想的，commons.js包括react和react-dom

- webpack.config.js

```js
var webpack = require('webpack');

module.exports = {
  entry: {
    bundle1: './main1.jsx',
    bundle2: './main2.jsx'
  },
  output: {
    filename: '[name].js'
  },
  module: {
    rules:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['es2015', 'react']
          }
        }
      },
    ]
  },
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: "commons",
      // (the commons chunk name)

      filename: "commons.js",
      // (the filename of the commons chunk)
    })
  ]
}
```

### Demo13:Vendor chunk

通过<font color=FF0000>CommonsChunkPlugin</font>,你能从JS脚本提取官方库到单独的文件中

- main.js

```js
var $ = require('jquery');
$('h1').text('Hello World');
```

- index.html

```html
<html>
  <body>
    <h1></h1>
    <script src="vendor.js"></script>
    <script src="bundle.js"></script>
  </body>
</html>
```

- webpack.config.js

```js
var webpack = require('webpack');

module.exports = {
  entry: {
    app: './main.js',
    vendor: ['jquery'],
  },
  output: {
    filename: 'bundle.js'
  },
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: 'vendor',
      filename: 'vendor.js'
    })
  ]
};
```

在上面的代码中，<font color=FF0000>entry.vendor:['jquery']</font>告诉Webpack，<font color=FF0000>jquery</font>应该被包括到通用块<font color=FF0000>vendor</font>.js中。

如果你想要一个模块作为全局变量来在不同的模块中使用，比如不用在每个文件中<font color=FF0000>require</font>('jquery')</font>，而是让<font color=FF0000>$</font>或者<font color=FF0000>jQuery</font>作为全局变量，需要使用<font color=FF0000>ProvidePlugin</font>，它能够自动加载模块而不需要到处<font color=FF0000>import</font>或者是<font color=FF0000>require</font>

```js
// main.js
$('h1').text('Hello World');


// webpack.config.js
var webpack = require('webpack');

module.exports = {
  entry: {
    app: './main.js'
  },
  output: {
    filename: 'bundle.js'
  },
  plugins: [
    new webpack.ProvidePlugin({
      $: 'jquery',
      jQuery: 'jquery'
    })
  ]
};
```

在Demo13中，你需要自己全局加载jquery.js

### Demo14:公开全局变量

如果你想用一些全局变量，不需要在Webpack包中包含他们，你可以使用webpack.config.js里的<font color=FF0000>externals</font>字段

- data.js

```js
// data.js
var data = 'Hello World';
```

- index.html

```html
<html>
  <body>
    <script src="data.js"></script>
    <script src="bundle.js"></script>
  </body>
</html>
```
> 注意，Webpack只会构建bundle.js, 而不会构建data.js

```js
// webpack.config.js
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    rules:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['es2015', 'react']
          }
        }
      },
    ]
  },
  externals: {
    // require('data') is external and available
    //  on the global var data
    'data': 'data'
  }
};
```

此时，你可以require('data')作为模块变量，实际上它是一个全局变量

```js
// main.jsx
var data = require('data');
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>{data}</h1>,
  document.body
);
```

同样可以将react和react-dom放入externals，这样显著的降低构建bundle.js的时间和文件大小

### Demo15:React router

