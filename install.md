# install
<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [安装 nodejs](#安装-nodejs)
  - [命令行安装](#命令行安装)
  - [添加源安装](#添加源安装)
  - [下载文件安装](#下载文件安装)
  - [查看版本](#查看版本)
  - [卸载](#卸载)
- [包管理](#包管理)
- [安装 gitbook](#安装-gitbook)
- [插件](#插件)
- [问题](#问题)
- [参考](#参考)

<!-- /code_chunk_output -->

<!-- [Toc] -->

> 说明：测试环境——ubuntu20

## 安装 nodejs

node.js中某版本对Gitbook支持好：`v12.16.3`版本支持很好，`v14.3.0`版本不OK


### 命令行安装

有人推荐以下指令，但我的不能用，也许你的能用：

```sh
# 直接安装在系统环境/usr/bin目录下，之后使用npm -g安装其他插件也会安装到/usr/lib/node_modules(需要使用sudo权限)。
sudo apt-get install nodejs-legacy nodejs  
```

提示信息：

```sh
Package nodejs-legacy is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source
However the following packages replace it:
  nodejs libnode64

E: Package 'nodejs-legacy' has no installation candidate
```

改用以下指令

```sh
# 将nodejs路径链接到/usr/local/bin目录下，则每次npm -g安装插件都会安装在nodejs原路径下的node_modules
# (比如/home/ubuntu/node-v8.1.0-linux-x64/lib/node_modules)，
# 每次代码中引用插件也需要到此目录下去找
sudo apt-get install npm nodejs  

# 查看版本
node -v  # 10.19.0
npm -v   # 6.14.4 
```

### 添加源安装

```sh
curl -fsSL https://deb.nodesource.com/setup_12.x | sudo -E bash - &&\
sudo apt-get install -y nodejs  # node:v12.22.12  npm:6.14.16
```

### 下载文件安装

```sh
# 下载
wget https://nodejs.org/dist/v8.1.0/node-v12.16.3-linux-x64.tar.xz
# 解压
tar -xvf node-v12.16.3-linux-x64.tar.xz
# 添加环境变量路径，若解压的全局路径为 /home/xxx/node-v12.16.3-linux-x64，则
export PATH=/home/xxx/node-v12.16.3-linux-x64/bin/:$PATH
```

### 查看版本

```sh
node -v  # v12.16.3
npm -v   # 6.14.4
```

### 卸载

```sh
sudo apt remove nodej*
sudo apt purge nodej*
sudo apt autoremove   # 这一步慎重，注意看删了哪些。如果会删除别的，则可以跳过该步
sudo rm -r /etc/apt/sources.list.d/nodesource.list
sudo rm -r /usr/local/lib/node_modules
sudo rm -r /usr/local/include/node/
sudo rm -r /usr/local/bin/node
sudo rm -r /tmp/npm* 
```

## 包管理

```sh
# 升级 nodejs 和 npm 版本
sudo npm install n -g
sudo n stable
npm i -g npm

# 配置 npm 镜像源为淘宝源；
npm config set registry http://registry.npm.taobao.org/
```



## 安装 gitbook

使用以下指令安装可能会卡住：

```sh
npm install gitbook -g
```

更改为以下指令安装没出问题：

```sh
npm uninstall -g gitbook
npm install -g gitbook-cli  
npm install gitbook-pdf -g    #(输出pdf
```

检查是否安装成功：  

```sh
node -v  
gitbook -V  # 若gitbook没安装，这一步会自动安装
```

## 插件

默认带有 5 个插件：

- highlight - 语法高亮插件
- search - 搜索插件，导航栏查询功能
- sharing - 分享插件，右上角分享功能
- font-settings - 字体设置插件（最上方的``"A"``符号）
- livereload - 热加载插件，为GitBook实时重新加载

**必备插件**：

- [anchor-navigation-ex]( https://github.com/zq99299/gitbook-plugin-anchor-navigation-ex)：导航扩展，增加锚点，返回顶部，显示序号。展示页面大纲的空间，可以按照段落来展示，可以快捷转挑到页面的相应位置。悬浮目录和回到顶部。
- [anchor-navigation](https://github.com/yaneryou/gitbook-plugin-anchor-navigation)：锚点导航(为什么不能用？)
- [donate](https://github.com/willin/gitbook-plugin-donate)：捐赠打赏按钮插件
- [splitter](https://github.com/yoshidax/gitbook-plugin-splitter)：在左侧目录和右侧内容之间添加一个可以拖拽的栏，用来调整两边的宽度。
- [tbfed-pagefooter](https://github.com/zhj3618/gitbook-plugin-tbfed-pagefooter)：自定义页脚，显示版权和最后修订时间。
- [ad](https://github.com/zhaoda/gitbook-plugin-ad)：在每个页面顶部和底部添加广告或任何自定义内容。

**常用插件**

- [editlink](https://github.com/zhaoda/gitbook-plugin-editlink)：内容顶部显示`编辑本页`链接。
- [book-summary-scroll-position-saver](https://github.com/yoshidax/gitbook-plugin-book-summary-scroll-position-saver)：自动保存左侧目录区域导航条的位置。
- [prism](https://github.com/gaearon/gitbook-plugin-prism)：基于 [Prism](http://prismjs.com/) 的代码高亮。
- [atoc](https://github.com/willin/gitbook-plugin-atoc)：插入 TOC 目录。
- [ace](https://github.com/ymcatar/gitbook-plugin-ace)：插入代码高亮编辑器。
- [include-codeblock](https://github.com/azu/gitbook-plugin-include-codeblock)：通过引用文件插入代码。
- [expandable-chapters](https://github.com/DomainDrivenArchitecture/gitbook-plugin-expandable-chapters)：收起或展开章节目录中的父节点。
- [page-treeview](https://www.npmjs.com/package/gitbook-plugin-page-treeview-simple) ：插件是生成页内目录
- page-treeview-simple：和 `page-treeview` 功能相同，在其基础之上修改了以下内容——去除 `copyRight` 的提示内容与占用的空白高和取消章节的折叠效果，默认展开显示完整章节
- [simple-page-toc](https://www.npmjs.com/package/gitbook-plugin-simple-page-toc) ：生成本页目录 需要在文章中插入标签，支持1-3级目录 页面顶端生成。另外 GitBook 在处理重复的标题时有些问题，所以尽量不适用重复的标题
- [page-toc](https://www.npmjs.com/package/gitbook-plugin-page-toc-af)：每个页面上添加了一个目录 (TOC)。您可以设置目录是否默认显示在所有页面上，您可以启用或禁用个别页面上的目录以覆盖默认值。
- ancre-navigation：右上角悬浮导航和回到顶部按钮
- intopic-toc：在右侧插入目录，文中不需要写 Toc
- [anchors](https://github.com/rlmv/gitbook-plugin-anchors)：标题带有 github 样式的锚点。
- [github](https://github.com/GitbookIO/plugin-github)：在右上角显示 github 仓库的图标链接。
- [github-buttons](https://github.com/azu/gitbook-plugin-github-buttons)：显示 github 仓库的 star 和 fork 按钮。
- page-toc-button：悬浮目录
- page-treeview
- donate：打赏
- flexible-alerts：警报
- klipse：嵌入类似IDE的功能

**可能有用的**

- [redirect](https://github.com/ketan/gitbook-plugin-redirect)：页面跳转(重定向)。
- [sectionx](https://github.com/ymcatar/gitbook-plugin-sectionx)：分离各个段落，并提供一个展开收起的按钮。
- [favicon](https://github.com/menduo/gitbook-plugin-favicon)：为网站添加了favicon和Apple Touch图标。
- [image-captions](https://github.com/todvora/gitbook-plugin-image-captions)：抓取内容中图片的 `alt` 或 `title` 属性，在图片下面显示标题。
- [mermaid](https://github.com/JozoVilcek/gitbook-plugin-mermaid)：使用流程图。
- [latex-codecogs](https://github.com/GitbookIO/plugin-latex-codecogs)：使用数学方程式。
- [disqus](https://github.com/GitbookIO/plugin-disqus)：添加 disqus 评论插件。
- [sitemap](https://github.com/GitbookIO/plugin-sitemap)：生成站点地图。
- [baidu](https://github.com/poppinlp/gitbook-plugin-baidu)：使用百度统计。
- [ga](https://github.com/GitbookIO/plugin-ga)：添加 Google 统计代码。
- [duoshuo](https://github.com/codepiano/gitbook-plugin-duoshuo)：使用多说评论。
- [prism](https://github.com/gaearon/gitbook-plugin-prism)：基于 Prism 的代码高亮
- alerts：主要是一些样式的插件，可以根据配置针对不同的内容定义不同的颜色。
- [disqus](https://github.com/GitbookIO/plugin-disqus)：评论插件，需要注册disqus.com账号，[使用例程](https://blog.csdn.net/weixin_38171180/article/details/100689129;)

**一般用不到的**

- [chart](https://github.com/csbun/gitbook-plugin-chart)：使用 C3.js 图表。
- [youtubex](https://github.com/ymcatar/gitbook-plugin-youtubex)：插入 YouTube 视频。
- [fbqx](https://github.com/Erwin-Chan/gitbook-plugin-fbqx)：使用填空题。
- [mcqx](https://github.com/ymcatar/gitbook-plugin-mcqx)：使用选择题，交互式多选
- [spoiler](https://github.com/ymcatar/gitbook-plugin-spoiler)：隐藏答案，当鼠标划过时才显示。
- [styles-sass](https://github.com/GitbookIO/plugin-styles-sass)：使用 SASS 替换 CSS。
- [styles-less](https://github.com/GitbookIO/plugin-styles-less)：使用 LESS 替换 CSS。

去除默认插件，可以在插件名称前面加 `-`

- 官方获取插件地址： https://plugins.gitbook.com/（现在已经无法访问了）。
- 插件其他地址：https://www.npmjs.com/search?q=gitbook

安装插件只须在书籍目录下修改 book.json 文件，在`book.json`写入相应插件`plugins`和配置`pluginsConfig`后，使用`gitbook install`安装插件。例如增长折叠目录的插件，须在 book.json 内增加下面代码:

```json
{
    "plugins": ["expandable-chapters-small"],
    "pluginsConfig": {
        "expandable-chapters-small":{}
    }
}
```

而后终端执行命令 `gitbook install` 来安装插件便可。如果使用该命令安装较慢，可使用npm安装：

```sh
npm install gitbook-plugin-plugin_name 
# 如插件：expandable-chapters-small
npm install gitbook-plugin-expandable-chapters-small
```

> 注意：安装位置在当前目录下的 node_modules 文件夹中。

**常见插件配置**

```json
{
    // 如果希望将网页源码暴露出去并接受公众的监督校准的话,使用edit-link插件可以直接链接到源码文件
    "plugins": ["edit-link"],	
    "pluginsConfig": {	
        "edit-link": {	
          "base": "https://github.com/snowdreams1006/snowdreams1006.github.io/blob/master",	
          "label": "编辑本页"	
        }	
    },
    // 在左上角插入一个logo图片的插件，就像上面截图中的一样，可以插入自己的logo图片	
    "plugins": [ "insert-logo" ],
    "pluginsConfig": {
        "insert-logo": {
            "url": "https://fangjian98.gitee.io/gitbook/images/android.png",
            "style": "background: none; max-height: 30px; min-height: 30px"
        }
    },
    // insert-logo 插入logo
    "plugins": [ "insert-logo" ],
    "pluginsConfig": {
      "insert-logo": {
        "url": "images/logo.png",
        "style": "background: none; max-height: 30px; min-height: 30px"
      }
    },
    // hide-element 隐藏元素：默认的gitbook左侧提示：Published with GitBook
	"plugins": [ "hide-element" ],
    "pluginsConfig": {
        "hide-element": {
            "elements": [".gitbook-link"]
        }
    },
    // back-to-top-button 回到顶部
    "plugins": [ "back-to-top-button" ],
	// chapter-fold 导航目录折叠，gitbook默认目录没有折叠效果
	"plugins": ["chapter-fold"],
	// 或者 expandable-chapters-small
	"plugins": ["expandable-chapters-small"],
    "pluginsConfig": {
        "expandable-chapters-small":{}
    },
    "plugins": ["atoc", "splitter"],
    "pluginsConfig": {
        "atoc": {
               "addClass": true,
               "className": "atoc"
           }
    },
	// code 复制代码
	"plugins" : [ "code" ],
	// splitter 侧边栏宽度可调节
	"plugins": [ "splitter" ],
	// search-pro 高级搜索：支持中英文，准确率更高一些
	"plugins": [
          "-lunr", 
          "-search", 
          "search-pro"
    ],
    // pageview-count 阅读量计数：记录每个文章页面被访问的次数
    "plugins": [ "pageview-count"],
    // custom-favicon 修改标题栏图标：设置浏览器选项卡标题栏的小图标，注意只支持ico后缀的图片，并且只支持本地图片，不支持网络图片链接。图标的分辨率要是32x32的。
    "plugins" : ["custom-favicon"],
    "pluginsConfig" : {
        "favicon": "icon/favicon.ico"
    }
    // tbfed-pagefooter 页面添加页脚，在每个文章下面标注版权信息和文章时间
    "plugins": [
       "tbfed-pagefooter"
    ],
    "pluginsConfig": {
        "tbfed-pagefooter": {
            "copyright":"Copyright &copy dsx2016.com 2019",
            "modify_label": "该文章修订时间：",
            "modify_format": "YYYY-MM-DD HH:mm:ss"
        }
    },
	// popup 弹出大图：点击可以在新窗口展示图片
	"plugins": [ "popup" ],
	// sharing-plus 分享当前页面，gitbook默认只有Facebook、Google+、Twiter、Weibo、Instapaper，插件可以有更多分享方式，也可以关闭指定分享方式。
	"plugins": ["-sharing", "sharing-plus"],
    "pluginsConfig": {
        "sharing": {
             "douban": true,
             "facebook": true,
             "google": true,
             "pocket": true,
             "qq": true,
             "qzone": true,
             "twitter": true,
             "weibo": true,
          "all": [
               "douban", "facebook", "google", "instapaper", "linkedin","twitter", "weibo", 
               "messenger","qq", "qzone","viber","whatsapp"
           ]
       }
    },
	// change_girls 可自动切换的背景
	"plugins":["change_girls"],
    "pluginsConfig": {
        "change_girls" : {
            "time" : 5,
            "urls" : [
                "girlUrl1", "girlUrl2",...
            ]
        }
    },
    // emphasize强调突出颜色
    "plugins": ["emphasize"],
    // This text is {% em %}highlighted !{% endem %}
    // This text is {% em %}highlighted with **markdown**!{% endem %}
    // This text is {% em type="green" %}highlighted in green!{% endem %}
    // This text is {% em type="red" %}highlighted in red!{% endem %}
    // This text is {% em color="#ff0000" %}highlighted with a custom color!{% endem %}
        
    // sidebar-style 导航栏显示作者信息
    "plugins": ["sidebar-style"],
    "pluginsConfig": {
        "sidebar-style": {
            "title": "前端开发",
            "author": "付铭"
        }
    }，
    // 只会提取h[1-3]标签作为悬浮导航，只有按照以下顺序嵌套才会被提取：必须要以 h1 开始，直接写 h2 不会被提取
    // anchor-navigation-ex和别的插件会互相叠加影响，应选择其中一种即可
    plugins: ["anchor-navigation-ex"],
    pluginsConfig: [
        "anchor-navigation-ex": {
        "tocLevel1Icon": "fa fa-hand-o-right",
        "tocLevel2Icon": "fa fa-hand-o-right",
        "tocLevel3Icon": "fa fa-hand-o-right",
        "multipleH1": false,
        "multipleH2": false,
        "multipleH3": false,
        "multipleH4": false,
        "showLevelIcon": false,
        "showLevel": false
    },
	// page-toc-button
	// maxTocDept 标题的最大深度（2 = h1 + h2 + h3）。不支持值> 2。 默认2
	// minTocSize 显示toc按钮的最小toc条目数。 默认 2
	"pluginsConfig": {
        "page-toc-button": {
            "maxTocDepth": 2,
            "minTocSize": 2
       }
	}
    // 嵌入类似IDE的功能
    "plugins": ["klipse"],
	// 在 markdown 中插入代码段
        // eval-python
        //     print [x + 1 for x in range(10)]
    
}
```

> 注意：配置文件中不能有注释，也不能有多余的逗号，否则会报错。json在发明之初就是不提倡注释的。



## 问题

1. `gitbook init` 报错：`TypeError [ERR_INVALID_ARG_TYPE]: The "data" argument must be of type string or an instance of Buffe`

   **解决：** 更换 nodejs 较低版本

2. `npm install gitbook-pdf -g` 安装phantomjs出错：

   ```sh
   Phantom installation failed { Error: EACCES: permission denied, link '/tmp/phantomjs/phantomjs-2.1.1-linux-x86_64.tar.bz2-extract-1496325965675/phantomjs-2.1.1-linux-x86_64' -> '/XXX/node_modules/phantomjs-prebuilt/lib/phantom'
   at Error (native)
   errno: -13,
   code: 'EACCES',
   syscall: 'link',
   path: '/tmp/phantomjs/phantomjs-2.1.1-linux-x86_64.tar.bz2-extract-1496325965675/phantomjs-2.1.1-linux-x86_64',
   dest: '/XXX/node_modules/phantomjs-prebuilt/lib/phantom' } Error: EACCES: permission denied, link '/tmp/phantomjs/phantomjs-2.1.1-linux-x86_64.tar.bz2-extract-1496325965675/phantomjs-2.1.1-linux-x86_64' -> '/XXX/node_modules/phantomjs-prebuilt/lib/phantom'
   at Error (native)
   npm ERR! code ELIFECYCLE
   npm ERR! errno 1
   npm ERR! phantomjs-prebuilt@2.1.14 install: `node install.js`
   npm ERR! Exit status 1
   ```

   **解决方法：**

   ```sh
   rm -rf node_modules                       #（删除前面构建错的目录，如果没有安装到/usr下）
   npm install gitbook-pdf -g --unsafe-perm  #（重新构建）
   ```

   

## 参考

1. [Gitbook部署之nodejs踩坑](https://www.cnblogs.com/hacv/p/14311409.html)
2. [ElasticSearch 安装时一些错误以及解决方法 ](https://www.cnblogs.com/frank-hui/p/12200284.html)
3. https://github.com/nodesource/distributions
4. [关于gitbook的结构及优化配置](https://blog.csdn.net/weixin_44008788/article/details/113920083)
5. https://www.mapull.com/gitbook/comscore/custom/plugin/common/toc.html
6. https://www.zhaowenyu.com/gitbook-doc/
7. [GitBook使用教程](https://www.dandelioncloud.cn/article/details/1575108888532054017)
8. [gitook 插件 文章目录导航 ](https://blog.51cto.com/ghostwritten/5357717)
9. [gitbook 插件 文章 TOC 目录](https://blog.csdn.net/xixihahalelehehe/article/details/125117549)
10. [Gitbook 打造的 Gitbook 说明文档](https://www.mapull.com/gitbook/comscore/)
10. [官方文档 - 使用GitBook和Typora生成类似官方文档](https://www.cnblogs.com/h-z-y/p/14437348.html)：该博客给出了很多插件的源码地址
