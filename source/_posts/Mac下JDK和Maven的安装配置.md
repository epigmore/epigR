title: Mac下JDK和Maven的安装配置
date: 2015-11-26 19:54:50
categories: 程序开发
tags: JAVA
---

### 从Oracle官网下载最新版本JDK
选择Mac OSX版点击安装，安装完成后在终端中输入

``` bash
$ java -version
```
出现JDK版本号说明安装成功。

``` bash
$ vim .bash_profile
```
JDK默认安装路径在/Library/Java/JavaVirtualMachines/目录下
接下来需要配置JAVA_HOME变量

> export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_65.jdk/Contents/Home"

### 安装Maven
从apache官网选择需要的Maven版本下载
解压到~/Library/Maven

配置Maven环境变量
export M2_HOME="~/Library/Maven/apache-maven-3"
export PATH=$PATH:$M2_HOME/bin

### 测试
现在可以创建一个Maven项目进行测试。。。