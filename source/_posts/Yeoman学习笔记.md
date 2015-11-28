title: Yeoman学习笔记
date: 2015-11-21 23:06:19
categories: 程序开发
tags: Yeoman
---

## Yeoman介绍
Yeoman是Google的团队和外部贡献者团队合作开发的，他的目标是通过Grunt（一个用于开发任务自动化的命令行工具）和Bower（一个HTML、CSS、Javascript和图片等前端资源的包管理器）的包装为开发者创建一个易用的工作流。

Yeoman的目的不仅是要为新项目建立工作流，同时还是为了解决前端开发所面临的诸多严重问题，例如零散的依赖关系。

Yeoman主要有三部分组成：yo（脚手架工具）、grunt（构建工具）、bower（包管理器）。这三个工具是分别独立开发的，但是需要配合使用，来实现我们高效的工作流模式。

## 安装过程
Yeoman需要NodeJS、Ruby和Compass环境

1、下载安装NodeJS

2、Mac下已经自带了Ruby环境

3、Compass安装依赖于Ruby

执行命令

``` bash
sudo gem install compass
```
4、安装Yeoman

执行命令

``` bash
sudo npm install -g yo grunt-cli bower
```
在这里需要说一下grunt-cli,grunt是非常有名的基于node的javascript构建工具，grunt有自己的脚手架工具grunt-init,并且也有许多常用的模版，有兴趣的同学可以了解下。

5、安装模版

执行命令

``` bash
npm install -g [generator-webapp|generator-angular|generator-ember|generator-＊]
```

6、环境验证

``` bash
yo doctor
```

若出现下面说明环境安装完成

``` bash
Yeoman Doctor
Running sanity checks on your system

✔ Global configuration file is valid
✔ NODE_PATH matches the npm root
✔ Node.js version
✔ No .bowerrc file in home directory
✔ No .yo-rc.json file in home directory
✔ npm version

Everything looks all right!

```

7、生成工程

执行命令创建基于webapp模版工程目录和安装工程依赖

``` bash
yo webapp
```
可能会出现有关phantomjs的错误，这是由于phantomjs工具托管的服务器被墙的原因，phantomjs是什么东东，可以自行上网搜索，本人是通过淘宝的镜像下载phantomjs的1.9.8版本手动安装并配置环境变量，phantomjs目前的最新版本是2.0.0，但是由于本人mac手动安装phantomjs的2.0.0版后无法运行，网上大神说是phantomjs的2.0.0版在Mac系统下的bug，果断放弃。



8、测试

执行命令

``` bash
grunt server
```
