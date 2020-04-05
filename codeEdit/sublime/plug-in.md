# Sublime插件

## 利用Package Control安装插件
- ctrl+shift+p或者菜单栏:Tools-->command palette调出命令面板, 输入install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件,在输入框中直接输入插件名称可进行搜插件,双击即可自动安装,退出命令面板,在重复的按两次ctrl+shift+p`可退回上次操作,或菜单栏上选择命令面板

## 如何查找已安装的插件
- 去除插件同样调出命令行面板ctrl+shift+p或者菜单栏Tools-->command Palette,拉动滚动条,可以查看插件所有的命令快捷操作,列出插件(list Packages),移除插件(remove Package)等，以Alignment对齐代码插件为例:先移除后安装,其他插件雷同,在线移除插件过程需要等待一段时间,移除后,可在preferences-->Package settings中插件插件的有无,第二种去除插件的方法就是直接去packages中间的插件文件夹删除掉就可以了的,一旦去除插件,对应的快捷键操作就消失了的

### 1.Emmet插件
- 采用了仿CSS选择器的语法将你输入的代码片段生成为完整的HTML或CSS代码，极大的提高了代码的编写速度。

### 2.CSSComb插件：
- 这款插件可以使用指定的排序方式对CSS的属性进行排序，使你的CSS代码更加规范
- 使用：右键 run CSScomb 即可

### 3.CSS Format插件:
- 强大的CSS格式工具，有多种格式可供选择
- 右键 CSS Format （注意，与CSScomb不同，不会改变CSS属性的顺序）

### 4.HTML-CSS-JS Prettify插件
- 前端通吃的格式优化插件 HTML-CSS-JS Prettify
- 右键选择即可

### 5.自动补全css前缀：
- 下载autoprefix插件
- ctrl+shift+p

### 6.SublimeTmpl 快速生成文件模板SublimeTmpl 
- 能新建 html、css、javascript、php、python、ruby 六种类型的文件模板，所有的文件模板都在插件目录的templates文件夹里，可以自定义编辑文件模板，生成自己所需要的,一次性的配好模板,无需重复的输入一些毫无意义的劳动，一劳永益

```
SublimeTmpl默认的快捷键
ctrl+alt+h → html
ctrl+alt+j → javascript
ctrl+alt+c → css
ctrl+alt+p → php
ctrl+alt+r → ruby
ctrl+alt+shift+p → python
```

### 7.cssRem安装

- 自动将px转化为rem的插件,做移动端网站,rem布局时,该插件就很方便了

- 安装好后,设置基准值:"px_to_rem":数值,我这里设置是100也就是100px=1rem，具体得设置值根据你的适配而定

### 8.SublimeOnSaveBuild保存自动编译保存自动编译 
- SublimeOnSaveBuild(如果没有安装这个插件,每次都要手动的重新编译一次,ctrl+B),通过sass,less编译的css一般都是压缩的,在一行显示,若想要换行显示,右键执行run csscomb,让css自动排序

### 9.AutoprefixerCSS3 私有前缀自动补全插件，显然也是很有用的
- 设置快捷键，选择菜单Preferences > Key Bindings – User ,按照规则,将下面代码添加到里面去

```
{ "keys": ["ctrl+alt+shift+p"], "command": "autoprefixer" }
```

### 10.Colorpicker取色器插件

- 使用一个取色器改变颜色 使用方法: ctrl + shift + c
