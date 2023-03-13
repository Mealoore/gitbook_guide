# install

[Toc]

> 说明：测试环境——ubuntu20

## 安装 nodejs

node.js中某版本对Gitbook支持好：`v12.16.3`版本支持很好，`v14.3.0`版本不OK

### 命令行安装

有人推荐以下指令，但我的不能用，也许你的能用：

```sh
sudo apt-get install nodejs-legacy nodejs  # 直接安装在系统环境/usr/bin目录下，之后使用npm -g安装其他插件也会安装到/usr/lib/node_modules(需要使用sudo权限)。
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
sudo apt-get install npm nodejs  # 将nodejs路径链接到/usr/local/bin目录下，则每次npm -g安装插件都会安装在nodejs原路径下的node_modules(比如/home/ubuntu/node-v8.1.0-linux-x64/lib/node_modules)，每次代码中引用插件也需要到此目录下去找

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
- search - 搜索插件
- sharing - 分享插件
- font-settings - 字体设置插件
- livereload - 热加载插件

**必备插件**：

- [anchor-navigation-ex](https://plugins.gitbook.com/plugin/anchor-navigation-ex)：导航扩展，增加锚点，返回顶部，显示序号
- [anchor-navigation](https://plugins.gitbook.com/plugin/anchor-navigation)：锚点导航(为什么不能用？)
- [donate](https://plugins.gitbook.com/plugin/donate)：捐赠打赏按钮插件
- [splitter](https://plugins.gitbook.com/plugin/splitter)：在左侧目录和右侧内容之间添加一个可以拖拽的栏，用来调整两边的宽度。
- [tbfed-pagefooter](https://plugins.gitbook.com/plugin/tbfed-pagefooter)：自定义页脚，显示版权和最后修订时间。
- [ad](https://plugins.gitbook.com/plugin/ad)：在每个页面顶部和底部添加广告或任何自定义内容。

**常用插件**

- [editlink](https://plugins.gitbook.com/plugin/editlink)：内容顶部显示`编辑本页`链接。
- [book-summary-scroll-position-saver](https://plugins.gitbook.com/plugin/book-summary-scroll-position-saver)：自动保存左侧目录区域导航条的位置。
- [prism](https://plugins.gitbook.com/plugin/prism)：基于 [Prism](http://prismjs.com/) 的代码高亮。
- [atoc](https://plugins.gitbook.com/plugin/atoc)：插入 TOC 目录。
- [ace](https://plugins.gitbook.com/plugin/ace)：插入代码高亮编辑器。
- [include-codeblock](https://plugins.gitbook.com/plugin/include-codeblock)：通过引用文件插入代码。
- [expandable-chapters](https://plugins.gitbook.com/plugin/expandable-chapters)：收起或展开章节目录中的父节点。
- [anchors](https://plugins.gitbook.com/plugin/anchors)：标题带有 github 样式的锚点。
- [github](https://plugins.gitbook.com/plugin/github)：在右上角显示 github 仓库的图标链接。
- [github-buttons](https://plugins.gitbook.com/plugin/github-buttons)：显示 github 仓库的 star 和 fork 按钮。

**可能有用的**

- [redirect](https://plugins.gitbook.com/plugin/redirect)：页面跳转(重定向)。
- [sectionx](https://plugins.gitbook.com/plugin/sectionx)：分离各个段落，并提供一个展开收起的按钮。
- [favicon](https://plugins.gitbook.com/plugin/favicon)：为网站添加了favicon和Apple Touch图标。
- [image-captions](https://plugins.gitbook.com/plugin/image-captions)：抓取内容中图片的 `alt` 或 `title` 属性，在图片下面显示标题。
- [mermaid](https://plugins.gitbook.com/plugin/mermaid)：使用流程图。
- [latex-codecogs](https://plugins.gitbook.com/plugin/latex-codecogs)：使用数学方程式。
- [disqus](https://plugins.gitbook.com/plugin/disqus)：添加 disqus 评论插件。
- [sitemap](https://plugins.gitbook.com/plugin/sitemap)：生成站点地图。
- [baidu](https://plugins.gitbook.com/plugin/baidu)：使用百度统计。
- [ga](https://plugins.gitbook.com/plugin/ga)：添加 Google 统计代码。
- [duoshuo](https://plugins.gitbook.com/plugin/duoshuo)：使用多说评论。

**一般用不到的**

- [chart](https://plugins.gitbook.com/plugin/chart)：使用 C3.js 图表。
- [youtubex](https://plugins.gitbook.com/plugin/youtubex)：插入 YouTube 视频。
- [fbqx](https://plugins.gitbook.com/plugin/fbqx)：使用填空题。
- [mcqx](https://plugins.gitbook.com/plugin/mcqx)：使用选择题。
- [spoiler](https://plugins.gitbook.com/plugin/spoiler)：隐藏答案，当鼠标划过时才显示。
- [styles-sass](https://plugins.gitbook.com/plugin/styles-sass)：使用 SASS 替换 CSS。
- [styles-less](https://plugins.gitbook.com/plugin/styles-less)：使用 LESS 替换 CSS。

去除默认插件，可以在插件名称前面加 `-`；当遇到「左侧的目录折叠」这种需求的时候，就用到 GitBook 插件了。**官方获取插件地址：** https://plugins.gitbook.com/
安装插件只须要在书籍目录下增长 book.json 文件，在`book.json`写入相应插件`plugins`和配置`pluginsConfig`后，使用`gitbook install`安装插件。例如增长 折叠目录 的插件，须要在 book.json 内增长下面代码:

```json
{
    "plugins": ["expandable-chapters-small"],
    "pluginsConfig": {
        "expandable-chapters-small":{}
    }
}
```

而后终端执行命令 `gitbook install` 来安装插件便可。

常见插件配置：

```json
{
    // gitbook-plugin-insert-logo 图标	
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
    // tbfed-pagefooter 页面添加页脚
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
	// 
}
```







## 问题

1. `gitbook init` 报错：`TypeError [ERR_INVALID_ARG_TYPE]: The "data" argument must be of type string or an instance of Buffe`

   **解决：**更换 nodejs 较低版本

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
3. [关于gitbook的结构及优化配置](https://blog.csdn.net/weixin_44008788/article/details/113920083)
