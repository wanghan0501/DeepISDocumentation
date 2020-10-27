# DeepISDocumentation
文档入口地址: https://panzhengo1.github.io/DeepISDocumentation/

本文档使用 [docsify](https://docsify.js.org/#/) 工具编写。与Gitbook相比，docsify无需build，不会生成静态html文件，是一个可以快速生成文档网站的工具。[docsify文档](https://docsify.js.org/#/quickstart) 介绍了使用该工具的方法，简单来说，你只需要全局安装命令行工具：

```javascript
npm i docsify-cli -g
```

然后将本仓库克隆至本地：

```javascript
git clone git@github.com:Qinyimin/DeepISDocumentation.git
```

然后运行本地服务器来预览本文档：
```javascript
docsify serve docs
```
## Co-edit Documentation
为了添加Markdown文件到本文档，你需要:
1. 将你编写Markdown文件保存至/docs目录下
2. 修改导航文件 _sidebar.md, 添加该文件的相对路径到目录中
3. 在 Part3/updateLog.md 中记录你的更改

> 在提交更改到Github之前，请使用docsify serve命令预览以确保你的md文件能够正常显示！


## Add Plugins
目前使用的docsify插件有：

|  Plugins    |   Function & Configuration   |
| ---- | ---- |
|   Full text search   |  [提供搜索功能](https://docsify.js.org/#/plugins?id=full-text-search)    |
|   Zoom image   |   [图片放大功能](https://docsify.js.org/#/plugins?id=zoom-image)   |
|   Copy to Clipboard   |   [代码片复制到剪贴板](https://docsify.js.org/#/plugins?id=copy-to-clipboard)   |
|   Table of Content   |  [在右侧显示目录](https://github.com/mrpotatoes/docsify-toc)    |

添加更多插件请参考：[awesome-docsify](https://github.com/docsifyjs/awesome-docsify#plugins),  [docsify plugins](https://docsify.js.org/#/plugins)

## Change Theme
目前使用的主题为：[docsify-themable Simple](https://jhildenbiddle.github.io/docsify-themeable/#/themes)
更多主题：[awesome-docsify](https://github.com/docsifyjs/awesome-docsify#themes)