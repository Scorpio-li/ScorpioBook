<!--
 * @LastEditors: lizhiliang
--> 
# VUE配置

## 1. 压缩

- 在我们开发的时候，为了方便调试，我们需要使用源码进行调试，但在生产环境，我们追求的更多的是加载更快，体验更好，这时候我们会将代码中的空格注释去掉，对待吗进行混淆压缩，只为了让js,css文件变得更小，加载更快。

- gzip是Web世界中使用的最为广泛的文件压缩算法，当前我们使用的大多数服务端(比如nginx)和客户端(比如chrome)都已经支持了这个算法，所以如果我们在打包Vue项目的时候，可以直接将所有的静态资源压缩为gzip,就可以极大的减少静态资源的大小，提升浏览器加载速度

### 1.1 配置

#### 1.1.1 添加vue.config.js 文件

在新建Vue项目中，默认是没有vue.config.js文件的，首先你需要在项目根目录新建一个vue.config.js文件，然后在文件中加入以下代码

```js
module.exports = {

}
```

#### 1.1.2 配置compression-webpack-plugin

- 安装 compression-webpack-plugin

```shell
yarn add compression-webpack-plugin -D
```

- 配置vue.config.js

```js
const CompressionWebpackPlugin = require('compression-webpack-plugin')
const isProd = process.env.NODE_ENV === 'production'
module.exports = {
  configureWebpack: config => {
    if (isProd) {
      // 配置webpack 压缩
      config.plugins.push(
        new CompressionWebpackPlugin({
          test: /\.js$|\.html$|\.css$/,
          // 超过4kb压缩
          threshold: 4096
        })
      )
    }
  }
}
```

## 2. 移动端适配

- 两种适配方式
    
    1. 一种是将px转换为rem
    
    2. 另一种是将px转换为vw,在开发项目时，我一般喜欢将px转换为vw

### 2.1 安装 postcss-px-to-viewport

```shell
yarn add postcss-px-to-viewport -D
```

### 2.2 配置移动端适配

- 在项目根目录下面新建文件postcss.config.js,然后将以下代码加入到文件内

```js
module.exports = {
  plugins: {
    autoprefixer: {},
    'postcss-px-to-viewport': {
      // 视窗的宽度，对应的是我们设计稿的宽度，我们公司用的是375
      viewportWidth: 375,
      // 视窗的高度，根据750设备的宽度来指定，一般指定1334，也可以不配置
      // viewportHeight: 1334,
      // 指定`px`转换为视窗单位值的小数位数
      unitPrecision: 3,
      // 指定需要转换成的视窗单位，建议使用vw
      viewportUnit: 'vw',
      // 指定不转换为视窗单位的类，可以自定义，可以无限添加,建议定义一至两个通用的类名
      selectorBlackList: ['.ignore'],
      // 小于或等于`1px`不转换为视窗单位，你也可以设置为你想要的值
      minPixelValue: 1,
      // 允许在媒体查询中转换`px`
      mediaQuery: false
    }
  }
}
```

## 3. 移动端调试：vConsole

### 3.1 安装vConsole

```shell
yarn add vConsole -S
```

### 3.2 在项目中使用

- 打开main.js，然后在里面加入下面这段代码
```js
// 开发环境下面使用vConsole进行调试
if (process.env.NODE_ENV === 'development') {
  const VConsole = require('vconsole')
  new VConsole()
}
```

## 4. 精简moment

- 使用过moment的同学一定知道，moment的locale语言包特别大，但是我们一般的项目只在国内用，也用不到那么多语言，是不是可以去掉呢？这时候你需要使用到webpack.IgnorePlugin。

- 在vue.config.js文件，你需要添加以下代码

```js
const webpack = require('webpack')
module.exports = {
  chainWebpack: config => {
    // 优化moment 去掉国际化内容
    config
    .plugin('ignore')
    // 忽略/moment/locale下的所有文件
    .use(new webpack.IgnorePlugin(/^\.\/locale$/, /moment$/)) 
  }
}
```

- 我们虽然按照上面的方法忽略了包含’./locale/'该字段路径的文件目录,但是也使得我们使用的时候不能显示中文语言了，这时候如果想用某一种语言应该怎么办呢?

```js
import moment from 'moment'
//手动引入所需要的语言包
import 'moment/locale/zh-cn';
// 指定使用的语言
moment.locale('zh-cn');
```

## 5. 生产环境删除console.log

- 开发环境为了调试，会添加大量的console.log，但如果console.log提交到生产环境里面，不仅仅会影响到代码执行性能，而且可能会泄露一些核心数据，所以我们更希望的是在生产环境，将所有的console.log清除掉

### 5.1 安装插件

- 需要安装babel-plugin-transform-remove-console插件

```shell
yarn add babel-plugin-transform-remove-console -D
```

### 5.2 配置babel.config.js

- 打开babel.config.js文件，然后在文件内添加

```js
// 所有生产环境
const prodPlugin = []

if (process.env.NODE_ENV === 'production') {
  
// 如果是生产环境，则自动清理掉打印的日志，但保留error 与 warn
  prodPlugin.push([
    'transform-remove-console',
    {
      // 保留 console.error 与 console.warn
      exclude: ['error', 'warn']
    }
  ])
}

module.exports = {
   plugins: [
     ...prodPlugin
   ]
}
```

## 6. 开启eslint,stylelint

### 6.1 安装依赖

在配置这些lint之前，你需要安装这些插件

- @vue/cli-plugin-eslint

- @vue/eslint-config-prettier

- eslint-plugin-babel

- eslint-plugin-prettier

- eslint-plugin-vue

- husky

- lint-staged

- prettier

- stylelint

- stylelint-config-recess-order

- stylelint-config-standard

- stylelint-prettier

- stylelint-scss

同时还需要给vscode以下插件

- eslint

- stylelint

- Prettier - Code formatter

### 6.2 配置vscode

在vscode的setting文件里面添加以下代码

```js
"eslint.enable":true,
"eslint.options": {
  "extensions":[
    ".js",
    ".vue",
    ".ts",
    ".tsx"
  ]
 },
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
  "css.validate": true,
  "scss.validate": true,
  "less.validate": true,
  "editor.codeActionsOnSave": {
     "source.fixAll": true
  },
```

### 6.3 配置eslint

首先在项目根目录下面添加 .eslintrc.js与.eslintignore文件

- 在.eslintrc.js文件内添加以下内容

```js
// 缩略版
module.exports = {
  root: true,
  globals: {
    process: true
  },
  parserOptions: {
    parser: 'babel-eslint',
    sourceType: 'module'
  },
  env: {
    browser: true,
    node: true,
    es6: true
  },
  extends: ['plugin:vue/recommended', 'eslint:recommended'],
  plugins: ['babel', 'prettier'],
  rules:{ 
    // 校验规则此处略
 }
}
```

- 在.eslintignore文件中添加以下代码

```js
.DS_Store
node_modules
/dist

# local env files
.env.local
.env.*.local

# Log files
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Editor directories and files
.idea
.vscode
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
```

- 配置完之后，在package.json的script里面添加

```js
"eslint": "vue-cli-service lint"
```

- 然后执行yarn eslint就可以对代码进行格式化，当然vscode也会在你保存文件的时候校验一次

### 6.4 配置stylelint

限制js与vue是不够的，还需要限制以下style,感觉这是自己给自己无限挖坑的举措，但是这东西越用越爽，一起来看看

- 首先在项目根目录下面新建.stylelintrc.js与.stylelintignore文件

- 在.stylelintrc.js文件中添加以下内容

```js
module.exports = {
  extends: ["stylelint-config-standard","stylelint-config-recess-order"],
  "plugins": [
    "stylelint-scss"
  ],
  rules: {
    // 校验规则略
  }
}
```

- .stylelintignore文件内容与.eslintignore文件内容一致

- 配置完之后，在package.json的script里面添加

```js
"stylelint": "stylelint src/**/*.{html,vue,css,sass,scss} --fix",
```

- 然后执行yarn stylelint就可以对样式进行格式化，当然vscode也会在你保存文件的时候校验一次

## 7. 配置husky

在eslint,stylelint配置完之后，写代码时候vscode会自动校验格式化代码， 但就怕有人用其他编辑器没有配置插件，将未校验的代码提交到仓库里面，导致所有人的代码都爆红，这时候就需要使用husky在提交代码时候进行校验。

在git提交代码时候，会触发一系列hook钩子函数，而husky就是一个Git hooks工具。lint-staged是一个在git暂存文件上运行linters的工具,为什么要用这个工具呢，因为我们在提交代码的时候，只需要对已经修改过的文件进行校验，不然检查所有文件，比较浪费时间。那我们改怎么配置呢？

- 只需要在package.json文件里面添加以下代码

```js
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged",
      "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
    }
  },
  "lint-staged": {
    "*.{js,vue}": [
      "vue-cli-service lint",
      "git add -A"
    ],
    "*.{html,vue,css,sass,scss}": [
      "yarn stylelint"
    ]
  }
```

这时候你如果执行git commit -m '提交描述'的时候，会发现提交之前会调用eslint与stylelint进行代码校验，校验失败无法提交


