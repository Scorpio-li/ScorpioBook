# ScorpioBook

A book about Common Use

## GItbook

### 1. 安装教程

1. 下载安装 Node.js(最好使用8.x版本)

2. 安装 GitBook
```js
$ npm install gitbook-cli -g
```

### 2. 初始化

```js
$ gitbook init

$ gitbook serve // 预览书籍

$ gitbook build // 生成网页不启动服务器
```

### 3. 配置

- title: 本书标题

- author: 本书作者

- description: 本书描述

- anguage: 本书语言，中文设置 "zh-hans" 即可

- gitbook: 指定使用的 GitBook 版本

- styles: 自定义页面样式

- structure: 指定 Readme、Summary、Glossary 和 Languages 对应的文件名

- links: 在左侧导航栏添加链接信息

- plugins: 配置使用的插件

- pluginsConfig: 配置插件的属性

### 4. SUMMARY.md

- 这个文件主要决定 GitBook 的章节目录，它通过 Markdown 中的列表语法来表示文件的父子关系

```js
# Summary

* [Introduction](README.md)
* [Part I](part1/README.md)
    * [Writing is nice](part1/writing.md)
    * [GitBook is nice](part1/gitbook.md)
* [Part II](part2/README.md)
    * [We love feedback](part2/feedback_please.md)
    * [Better tools for authors](part2/better_tools.md)
```

- 我们通过使用 标题 或者 水平分割线 将 GitBook 分为几个不同的部分，如下所示：

```js
# Summary

### Part I

* [Introduction](README.md)
* [Writing is nice](part1/writing.md)
* [GitBook is nice](part1/gitbook.md)

### Part II

* [We love feedback](part2/feedback_please.md)
* [Better tools for authors](part2/better_tools.md)

---

* [Last part without title](part3/title.md)
```

### 5. 插件

- GitBook 有 插件官网，默认带有 5 个插件，highlight、search、sharing、font-settings、livereload，如果要去除自带的插件， 可以在插件名称前面加 -
```js
"plugins": [
    "-search"
]
```

- 如果要配置使用的插件可以在 book.json 文件中加入即可，比如我们添加 plugin-github，我们在 book.json 中加入配置如下即可：
```js
{
    "plugins": [ "github" ],
    "pluginsConfig": {
        "github": {
            "url": "https://github.com/your/repo"
        }
    }
}
```

- 然后在终端输入 gitbook install ./ 即可。

## 发布

```js
gitbook build // 生成_book文件夹

npm run deploy // 将_book发布到gh-pages分支上
```

## 文档链接

- [GitBook 简明教程](http://www.chengweiyang.cn/gitbook)

- [GitBook Github](https://github.com/GitbookIO)

- [GitBook文档（中文版）](http://caibaojian.com/gitbook/)

- [Gitbook中文文档](http://gitbook.hushuang.me/)
