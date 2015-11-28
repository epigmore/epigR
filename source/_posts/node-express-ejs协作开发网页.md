title: node_express_ejs协作开发网页
date: 2015-11-24 20:45:23
categories: 程序开发
tags: NodeJS
---

## 介绍
Node.js是一个基于Chrome JavaScript运行时建立的平台， 用于方便地搭建响应速度快、易于扩展的网络应用。Express 是一个基于 Node.js 平台的极简、灵活的 web 应用开发框架，它提供一系列强大的特性，帮助你创建各种 Web 和移动设备应用。EJS是一个JavaScript模板库，用来从JSON数据中生成HTML字符串。

## 安装
首先假定你已经安装了 Node.js，接下来为你的应用创建一个目录，然后进入此目录并将其作为当前工作目录。

使用Express应用生成器可以快速创建应用程序骨架，可以通过以下命令安装Express应用生成器

``` bash
$ npm install express-generator -g
```
通过以下命令生成应用骨架

``` bash
$ express -e ejs_demo
```
> -e是添加ejs模版支持默认是jade,当然你也可以手动安装ejs模版

``` bash
$ npm install ejs --save
```

通过 npm install 命令安装依赖。

``` bash
$ cd ejs_demo
$ npm install
```
启动这个应用（MacOS 或 Linux 平台）：

``` bash
$ DEBUG=myapp npm start
```

Windows 平台使用如下命令：

``` bash
> set DEBUG=myapp & npm start
```

## 测试

然后在浏览器中打开 http://localhost:3000/ 网址就可以看到这个应用了。

## 总结

和 Express 兼容的模板引擎，比如 Jade，通过 res.render() 调用其导出方法 __express(filePath, options, callback) 渲染模板。

有一些模板引擎不遵循这种约定，Consolidate.js 能将 Node 中所有流行的模板引擎映射为这种约定，这样就可以和 Express 无缝衔接。

``` bash
app.set('views', './views'); //views, 放模板文件的目录
app.set('view engine', 'ejs'); //view engine, 模板引擎
```