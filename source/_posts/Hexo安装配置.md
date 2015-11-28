title: Hexo安装配置
date: 2015-11-19 23:37:18
categories: 程序开发
tags: Hexo
---
Mac下配置和在GitHub部署Hexo博客系统

关于[Hexo](http://hexo.io/)!
Hexo是一个基于NodeJS的博客生成系统！你能通过[GitHub](https://github.com/hexojs/hexo/issues)站点获取Hexo项目

## 部署Hexo本地环境
### 登陆github
新建仓库命名为
username.github.io
这样做的创建的仓库是Github Pages站点
仓库中master分支里的文件将会被用来生成 Github Pages 站点

不同于个人和组织github提供的还有项目的站点
站点文件存放在项目本身仓库的 gh-pages 分支中

### 安装NodeJS
你可以同过NodeJS官方网站获取安装包进行安装

### 安装Hexo 
建议全局安装

``` bash
$ npm install -g hexo
```

### Hexo环境配置
创建hexo的目录
我创建的hexo目录，所有以下操作都是基于工作目录hexo前提下

进入hexo目录
初始化hexo工程

``` bash
$ hexo init
```

当然你也可以指定目录将工程初始化到指定的目录中

``` bash
$ hexo init <folder>
```

安装工程依赖项
到工程目录中

``` bash
$ npm install
```

接着执行下面命令

``` bash
$ hexo g 
$ hexo s
```

在浏览器中打开[http://localhost:4000](http://localhost:4000)
看到效果了吧

## 部署到GitHub

首先你需要配置GitHub的SSH登陆信息，动手通过网上找配置方法

你需要在hexo项目根目录下的_config.yml文件中找到

``` bash
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type:
```

修改为

``` bash
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: git@github.com:username/username.github.io.git
  branch: master
```

执行

``` bash
$ hexo g
$ hexo d
```

如果出现错误Error github not found
执行

``` bash
$ npm install hexo-deployer-git --save
```
再次执行$hexo g和$hexo d命令

在Mac和Linux下命令执行过程中可能需要root权限

hexo常用命令
hexo g 启动生成
hexo s 启动本地服务
hexo d 发布到github