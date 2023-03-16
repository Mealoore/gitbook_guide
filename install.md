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



## 问题

1. `gitbook init` 报错：
    ```sh
    **[terminal]
    TypeError [ERR_INVALID_ARG_TYPE]: 
    **[error The "data" argument must be of type string or an instance of Buffe]
    ```

    **解决：** 更换 nodejs 较低版本

2. `npm install gitbook-pdf -g` 安装phantomjs出错：
    ```sh
    **[terminal]
    Phantom installation failed { Error: EACCES: permission denied, link '/tmp/phantomjs/phantomjs-2.1.1-linux-x86_64.tar.bz2-extract-1496325965675/phantomjs-2.1.1-linux-x86_64' -> '/XXX/node_modules/phantomjs-prebuilt/lib/phantom'
    at Error (native)
    errno: -13,
    code: 'EACCES',
    syscall: 'link',
    path: '/tmp/phantomjs/phantomjs-2.1.1-linux-x86_64.tar.bz2-extract-1496325965675/phantomjs-2.1.1-linux-x86_64',
    dest: '/XXX/node_modules/phantomjs-prebuilt/lib/phantom' } Error: EACCES: permission denied, link '/tmp/phantomjs/phantomjs-2.1.1-linux-x86_64.tar.bz2-extract-1496325965675/phantomjs-2.1.1-linux-x86_64' -> '/XXX/node_modules/phantomjs-prebuilt/lib/phantom'
    at Error (native)
    **[error npm ERR! code ELIFECYCLE]
    **[error npm ERR! errno 1]
    **[error npm ERR! phantomjs-prebuilt@2.1.14 install: `node install.js`]
    **[error npm ERR! Exit status 1]

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
4. https://www.mapull.com/gitbook/comscore/custom/plugin/common/toc.html
5. https://www.zhaowenyu.com/gitbook-doc/
6. [Gitbook 打造的 Gitbook 说明文档](https://www.mapull.com/gitbook/comscore/)
