# Introduction

* [Introduction](README.md)
* [install](install.md)
* [usage](usage.md)



GitBook命令行工具是基于Node.js开发的，通过命令行可以创建、编辑和管理电子书。GitBook是目前最流行的开源书籍写作工具，其在写作方面主要有以下几点优势。

1. 支持Markdown和AsciiDoc语法。
2. 支持多语言，支持变量、模板和模板继承。
3. 可以导出静态站点或电子书（支持PDF、ePub、mobi等格式）。
4. 有丰富的插件。
5. 可以使用Git管理写作内容，方便多人协作和版本管理。
6. 可以将内容托管在GitHub或Gitlab中。 

使用GitBook可以搭建公司内部文档，用于内部的资料共享；也可以发布开源电子书，用于在互联网上分享知识。


**制作流程**

1. 环境配置：安装GitBook前需要先安装Node.js，然后再通过命令来安装GitBook。
2. 初始化工作目录`gitbook init`：初始化完成后会创建两个md格式的文件——README. md和SUMMARY. md
3. 写作过程：推荐的写作工具组合是：GitBook（书籍管理）+Typora（编辑器）+SourceTree（版本控制，Git可视化管理工具），对于编写和管理电子书来说，这是一种非常高效的组合。当然，使用VS Code也是一个不错的选择。
4. 编译生成`gitbook build`
5. 启动服务`gitbook serve`：打开一个Web服务器，默认监听4000端口
6. 查看效果：用浏览器打开 http://localhost:4000 查看书籍站点的显示效果。
7. 发布电子书：GitBook不仅可以生成静态网站，也可以生成3种格式（即ePub、mobi、PDF）的电子书。
8. 发布上线：如果想要开源，可以把书籍托管到GitHub上，然后绑定自己的域名。
