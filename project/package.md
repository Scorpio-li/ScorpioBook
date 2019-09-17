[npm总结](http://blog.csdn.net/u011240877/article/details/76582670)

[npm官网](https://www.npmjs.com/ )

## 1.什么是 npm？
- 官方文档介绍：npm makes it easy for JavaScript developers to share and reuse code, and it makes it easy to update the code that you’re sharing. ==>（npm 是一个包管理器，它让 JavaScript 开发者分享、复用代码更方便（有点 maven 的感觉哈））
- 可以重复的框架代码被称作包（package）或者模块（module），一个包可以是一个文件夹里放着几个文件，同时有一个叫做 package.json 的文件。
- npm 的作用就是让我们发布、下载一些 JS 轮子更加方便。
    1. 一个网站，就是前面提到用于搜索 JS模块的网站：[npm](https://www.npmjs.com/)
    2. 一个仓库，保存着人们分享的 JS 模块的大数据库
    3. 命令行里的客户端，开发者使用它来管理、安装、发布模块

## 2. 安装 npm
- npm 是依附于 node.js 的，我们可以去它的[官网](https://nodejs.org/en/download/) 下载安装 node.js。

## 3.更新 npm

```
npm install npm@latest -g
```
- npm@latest 就是 <packageName>@<version> 的格式，我们在下载其他模块时也是这个格式。-g 代表全局安装。

## 4.package.json 文件
- 管理本地安装 npm 包的最好方式就是创建 package.json 文件。
- 作用
    1. 作为一个描述文件，描述了你的项目依赖哪些包
    2. 允许我们使用“语义化版本规则”（后面介绍）指明你项目依赖包的版本
    3. 让你的构建更好地与其他开发者分享，便于重复使用

### package.json 如何创建
- 使用 npm init 即可在当前目录创建一个 package.json 文件：
![image](http://img.blog.csdn.net/20170802161624268?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMTI0MDg3Nw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### package.json 的内容
- package.json 文件至少要有两部分内容：

    1. “name”
        - 全部小写，没有空格，可以使用下划线或者横线
    2. “version”
        - x.x.x 的格式
        - 符合“语义化版本规则”
```
{
  "name": "shixinzhang-demo-package",
  "version": "1.0.0"
}
```

- 其他内容：

    1. description：描述信息，有助于搜索
    2. main: 入口文件，一般都是 index.js
    3. scripts：支持的脚本，默认是一个空的 test
    4. keywords：关键字，有助于在人们使用 npm search 搜索时发现你的项目
    5. author：作者信息
    6. license：默认是 MIT
    7. bugs：当前项目的一些错误信息，如果有的话
```s
我们可以为 init 命令设置一些默认值，比如：
> npm set init.author.email "shixinzhang2016@gmail.com"
> npm set init.author.name "shixinzhang"
> npm set init.license "MIT"
```

- 如果 package.json 中没有 description 信息，npm 使用项目中的 README.md 的第一行作为描述信息。这个描述信息有助于别人搜索你的项目，因此建议好好写 description 信息。


## 5.指定依赖的包
- 我们需要在 package.json 文件中指定项目依赖的包，这样别人在拿到这个项目时才可以使用 npm install 下载。
- 包有两种依赖方式：

    1. dependencies：在生产环境中需要用到的依赖
    2. devDependencies：在开发、测试环境中用到的依赖


## 6. Semantic versioning（语义化版本规则）
- dependencies 的内容，以 "weex-html5": "^0.3.2" 为例，我们知道 key 是依赖的包名称，value 是这个包的版本。那版本前面的 ^ 或者版本直接是一个 * 是什么意思呢？
- 这就是 npm 的 “Semantic versioning”，简称”Semver”，中文含义即“语义化版本规则”。

-  npm 包提供者应该注意的版本号规范。
-  如果一个项目打算与别人分享，应该从 1.0.0 版本开始。以后要升级版本应该遵循以下标准：

    1. 补丁版本：解决了 Bug 或者一些较小的更改，增加最后一位数字，比如 1.0.1
    2. 小版本：增加了新特性，同时不会影响之前的版本，增加中间一位数字，比如 1.1.0
    3. 大版本：大改版，无法兼容之前的，增加第一位数字，比如 2.0.0

- npm 包使用者就可以针对自己的需要填写依赖包的版本规则。
- 作为使用者，我们可以在 package.json 文件中写明我们可以接受这个包的更新程度（假设当前依赖的是 1.0.4 版本）：

    1. 如果只打算接受补丁版本的更新（也就是最后一位的改变），就可以这么写：
        - 1.0
        - 1.0.x
        - ~1.0.4
    2. 如果接受小版本的更新（第二位的改变），就可以这么写：
        - 1
        - 1.x
        - ^1.0.4
    3. 如果可以接受大版本的更新（自然接受小版本和补丁版本的改变），就可以这么写：
        - *
        - x


## 7.安装 package
- 使用 npm 安装 package 有两种方式：本地（当前项目路径）安装 或者 全局安装。
 
    1. 如果你只是想在当前项目里用 require() 加载使用，那你可以安装到本地
        npm install 默认就是安装到本地的
    2. 如果你想要在命令行里直接使用，比如 grunt CLI，就需要安装到全局了

- npm install 默认会安装 package.json 中 dependencies 和 devDependencies 里的所有模块。
- 如果想只安装 dependencies 中的内容，可以使用 --production 字段：
```s
npm install --production
```

### 本地安装 package
- npm 使用下面的命令下载一个包：npm install <package_name>

- 这个命令会在当前目录创建一个 node_modules 目录，然后下载我们指定的包到这个目录中。
- npm install 默认安装最新版本，如果想要安装指定版本，可以在库名称后加 @版本号：
```s
$ npm install sax@latest
$ npm install sax@0.1.1
$ npm install sax@">=0.1.0 <0.2.0"
```
#### 安装参数 --save 和 --save -dev
- 添加依赖时我们可以手动修改 package.json 文件，添加或者修改 dependencies devDependencies 中的内容即可。

- 另一种更酷的方式是用命令行，在使用 npm install 时增加 --save 或者 --save -dev 后缀：

    1. npm install <package_name> --save 表示将这个包名及对应的版本添加到 package.json的 dependencies
    2. npm install <package_name> --save-dev 表示将这个包名及对应的版本添加到 package.json的 devDependencies

#### 更新本地 package
- 有时候我们想知道依赖的包是否有新版本，可以使用 npm outdated 查看，如果发现有的包有新版本，就可以使用 npm update <package-name> 更新它，或者直接 npm update 更新所有：

#### 卸载本地 package

- 卸载一个本地 package 很简单，npm uninstall <package-name> 即可：
- 官方文档说输入 npm uninstall --save lodash 才能在删除项目的同时移除 package.json 中对它的依赖。但我没加 --save 也达到了一样的效果，一脸懵逼。


### 全局安装 package
- npm install -g <package-name>

- 安装后可以使用 npm ls -g --depth=0 查看安装在全局第一层的包。
- 全局安装的权限问题
    1. sudo npm install -g jshint，使用 sudo 简单粗暴，但是治标不治本
    2. 修改 npm 全局默认目录的权限: 
        - 先获取 npm 全局目录：npm config get prefix，一般都是 /usr/local；
        - 然后修改这个目录权限为当前用户：
            ```
             sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}
            ```
    3. 使用其他包管理器帮你解决这个问题
        - 实在懒得弄可以直接卸载 node，然后使用 Homebrew 重装 node:brew install node 
### 更新全局的 package

- 想知道哪些包需要更新，可以使用 npm outdated -g --depth=0，然后使用 npm update -g <package>更新指定的包：
- 要更新所有全局包，可以使用 npm update -g，可以发现对比本地的，只是多了个 -g。

### 卸载全局 package
- 一句搞定：npm uninstall -g <package>


## 8.其他命令

### npm run
- npm 还可以直接运行 package.json 中 scripts 指定的脚本：
- npm run 会创建一个Shell，执行指定的命令，并临时将node_modules/.bin加入PATH 变量，这意味着本地模块可以直接运行。
- package.json 中的 scripts 执行的脚本是本地项目内 node_modules -> .bin 内的脚本。

### npm install from github
- npm install 也可以直接从 github 下载:$ npm install git://github.com/package/path.git#0.1.0

### npm info
- npm info <package-name> 可以查看指定包的信息：

### npm adduser
- npm adduser 用于在npmjs.com注册一个用户:
```
$ npm adduser
Username: YOUR_USER_NAME
Password: YOUR_PASSWORD
Email: YOUR_EMAIL@domain.com
```

### npm home/repo
- npm home <package-name>命令可以打开指定模块的主页；
- npm repo <package-name>命令则是打开指定模块的代码仓库。

### npm prune
- npm prune 可以检查出当前项目的 node_modules目录中，没有在 package.json里提到的模块。


### npm publish
- 写出可以复用的 JS 代码后，我们就可以将它发布到 npm 仓库上，类似 Github 的提交。
- 要想发布，首先需要使用 npm adduser向 npmjs.com申请用户名（当然去官网也可以）。

- 接着使用 npm login 在命令行中登录。

- 登录以后，就可以使用 npm publish命令发布
