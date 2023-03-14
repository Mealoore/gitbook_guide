# usage
<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=3 orderedList=false} -->

<!-- code_chunk_output -->

- [电子书创建(举例说明如下)](#电子书创建举例说明如下)
  - [1 创建电子书](#1-创建电子书)
  - [2 编辑电子书内容(使用到md语法)](#2-编辑电子书内容使用到md语法)
- [控制命令](#控制命令)
- [问题](#问题)
- [参考](#参考)

<!-- /code_chunk_output -->

<!-- [Toc] -->


## 电子书创建(举例说明如下)  

### 1 创建电子书  

```sh
mkdir TestBook  
cd TestBook  
gitbook init
```

自动生成以下文件，若已经有了也不会覆盖：

- README.md：书籍的介绍写在这个文件里；
- SUMMARY.md：书籍的目录结构在这里配置

### 2 编辑电子书内容(使用到md语法)  

gitbook基本结构

```sh
├── book.json
├── README.md
├── SUMMARY.md
├── chapter1/
|    ├── README.md
|    ├── something.md
├── chapter2/
|    ├── README.md
```

1. README.md此文件是简单的电子书介绍，可以把您所制作的电子书做一下简单的描述：  

   ```markdown
   # 简介  
   这是我的第一本使用 GitBook 制作的电子书。
   ```

2. SUMMARY.md此为电子书的导航目录文件，每当新增一个章节文件就需要向此文件中添加一条记录。

   ```markdown
   # Summary
   * [Introduction](README.md)  
   * [uitest 是什么](users/index.md)  
       * [如何使用 uitest](users/use.md)  
       * [如何编写自定义的测试用例](users/case.md)  
       * [browserjs API 文档](users/api.md)  
   * [uitest 开发者文档](devs/index.md)  
       * [browserjs 开发者文档](devs/browserjs.md)  
       * [utci 文档](devs/utci.md)  
       * [utserver & utclient 文档](devs/utserver.md)  
   * [相关文章沉淀](artical.md)  
   * [关于 gitbook](gitbook.md)
   ```

3. Glossary.md对于电子书内容中需要解释的词汇可在此文件中定义。词汇表会被放在电子书末尾。  

   ```markdown
   # 电子书  
   电子书是指将文字、图片、声音、影像等讯息内容数字化的出版物
   和植入或下载数字化文字、图片、声音、影像等讯息内容的集存储和显示终端于一体的手持阅读器。
   # Kindle  
   Amazon Kindle 是由 Amazon 设计和销售的电子书阅读器（以及软件平台）。
   用户可以通过无线网络使用 Amazon Kindle 购买、下载和阅读电子书、报纸、杂志、博客及其他电子媒体。
   ```

4. book.json 是电子书的配置文件，可以看作是电子书的“原数据”，比如 title、description、isbn、language、direction、styles ，基本配置如下：

   ```json
   {
       "title": "TestBook",  
       "author": "Jian Fangjian <fangjian98@gmail.com>",
       "description": "TestBook",  
       "language": "zh-tw",  
   }
   ```
   
   配置说明


| 变量  | 描述 |
| ---- | ---- |
|root           | 包含所有图书文件的根文件夹的路径，除了 book.json |
| structure     | 指定自述文件，摘要，词汇表等的路径  |
| title         | 您的书名，默认值是从 README 中提取出来的。在 GitBook.com 上，这个字段是预填的。|
| description   | 您的书籍的描述，默认值是从 README 中提取出来的。在 GitBook.com 上，这个字段是预填的。|
| author        | 作者名。在GitBook.com上，这个字段是预填的。|
| isbn          | 国际标准书号 ISBN       |
| language      | 本书的语言类型，默认值是 `en`，可选：en, ar, bn, cs, de, en, es, fa, fi, fr, he, it, ja, ko, no, pl, pt, ro, ru, sv, uk, vi, zh-hans, zh-tw |
| direction     | 文本阅读顺序。可以是 rtl （从右向左）或 ltr （从左向右），默认值依赖于 language 的值。  |
| gitbook       | 应该使用的GitBook版本，并接受类似于 `>=3.0.0` 的条件。  |
| links         | 在左侧导航栏添加链接信息  |
| plugins       | 要加载的插件列表         |
| pluginsConfig | 插件的配置   |
| styles        | 自定义页面样式， 默认情况下各generator对应的css文件`"styles": { "website": "styles/website.css", }`  |



## 控制命令

在 TestBook 目录下执行如下命令

```sh
gitbook build [书籍路径] [输出路径]  # 生成html静态网页文件：_book，其中 index.html 为入口文件
gitbook serve [--port 端口号] # 在网页中查看，浏览器中输入 *http://localhost:4000* 即可预览电子书内容
gitbook pdf ./ ./mybook.pdf    # 生成 pdf/epub/mobi 格式的电子书
gitbook epub ./ ./mybook.epub  # 生成epub格式
gitbook mobi ./ ./mybook.mobi  # 生成 mobi 格式
```

其他命令：

```sh
gitbook help            # 列出gitbook所有的命令
gitbook --help          # 输出gitbook-cli的帮助信息
gitbook ls              # 列出本地所有的gitbook版本
gitbook ls-remote       # 列出远程可用的gitbook版本
gitbook fetch 标签/版本号 # 安装对应的gitbook版本
gitbook update           # 更新到gitbook的最新版本
gitbook uninstall 2.0.1  # 卸载对应的gitbook版本
```



## 问题

1. `gitbook build`报错：

   ```sh
   TypeError: cb.apply is not a function
       at /usr/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js:287:18
   ```

   **解决办法：** 
   注释`/usr/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js` `文件中以下三行

   ```cpp
   //fs.stat = statFix(fs.stat)
   //fs.fstat = statFix(fs.fstat)
   //fs.lstat = statFix(fs.lstat)
   ```

   

## 参考

1. [gitbook安装过程中出现TypeError: cb.apply is not a function](https://blog.csdn.net/swy_swy_swy/article/details/118542847?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-118542847-blog-110948703.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-118542847-blog-110948703.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=1)
2. [gitbook电子书制作步骤（linux环境下）](http://www.taodudu.cc/news/show-4899270.html)
2. [Ubuntu 安装 Gitbook 步骤和使用方法详解 以及 阿里云基于 Gitbook 我的博客部署](http://www.javashuo.com/article/p-mqknmune-nv.html)
2. [Gitbook 简介 使用总结 MD](https://www.bbsmax.com/A/A2dm2xY7ze/)
2. [Ubuntu安装nodejs +Gitbook安装 +nginx部署](https://blog.csdn.net/weixin_42396197/article/details/124218369)
2. [Ubuntu 安装 Gitbook 步骤和使用方法详解 以及 阿里云基于 Gitbook 我的博客部署](http://www.javashuo.com/article/p-mqknmune-nv.html)
2. [《了不起的Markdown》第八章](https://blog.csdn.net/m0_47838348/article/details/119873442)：从创建到发布的完整流程
2. http://gitbook.zhangjikai.com/
2. http://shenweiyan.gitee.io/gitbook/
2. http://caibaojian.com/gitbook/
2. http://www.zhaowenyu.com/gitbook-doc/
2. https://www.liqingbo.cn/docs/gitbook/
2. https://www.mapull.com/gitbook/comscore/