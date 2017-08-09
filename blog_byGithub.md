title : 使用 github 搭建博客页面
date  : 2017/5/19

---

[参考教程](https://hexo.io/zh-cn/docs/setup.html)

<!--more-->

## 准备工作：

1. 安装 git ，参考《Git 学习笔记》

2. 安装 node.js：
    [下载地址1](https://nodejs.org/zh-cn/download/)，
    [下载地址2](http://nodejs.cn/download/)

3. 安装 Hexo 
```    
$ npm install -g hexo-cli
```

4. 在 github 上新建一个仓库：username.github.io

5. 上传一个 .html 文件


## 开始搭建：

新建一个 Hexo 工程，也就是新建一个博客
``` bash
// 创建博客工程的文件夹目录
$ hexo init <folder>

// 进入这个目录
$ cd <folder>

// 结束
$ npm install
```

新建完成后可以看到指定文件夹下有多个目录，着重了解以下几个：

1. _config.yml：网站的配置信息，每次更改之后要重新运行
2. source：存放用户资源
3. theme：主题文件夹，修改主题的时候会用到
4. public：第一次运行之后生成的目录，运行后 source 目录下的文件被解析（MarkDown文件和HTML文件）或拷贝到这里


主要命令：

`hexo server` ：运行本地的服务器，默认情况下，访问网址为：http://localhost:4000/。

`hexo generate` ：生成本地的 html 静态文件，放在 public 目录下

`hexo deploy` ：部署之前生成的静态文件到网站，博客就基本搭建好了

## 其他

### 配置

根目录下的 _config.yml 文件中配置参数，更改配置后要记得重启

### 修改主题

[主题参考网站](https://www.zhihu.com/question/24422335)

1. 克隆主题 到 博客根目录下的 themes 主题目录下，记得更爱主题文件夹名，不然会出现 "WARN No layout: index.html" 报错

2. 修改配置文件 _config.yml 中的 theme 为要使用的主题名

### BUG

出现了 error deployer not found:github 的错误
