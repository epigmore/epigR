title: Octopress安装配置
date: 2015-11-20 20:01:31
categories: 程序开发
tags: Octopress
---

MAC OS X 部署Octopress

1、安装xcode
xcode中带有git
OS X自带ruby
检查ruby版本
如果版本过低需要安装RVM更新ruby

2、使用git克隆octopress项目
git clone git://github.com/imathis/octopress.git octopress

3、环境配置
安装bundle
gem install bundle
有时需要使用sudo获取root权限
如果安装无法从https://rubygems.org/源下载切换到淘宝的镜像源
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/

进入octopress目录
安装依赖
bundle install

如果出现
An error occurred while installing rake (10.4.2), and Bundler cannot continue.
Make sure that `gem install rake -v '10.4.2'` succeeds before bundling.
错误

执行
gem install rake -v '10.4.2'
升级安装rake

如果出现
Make sure that `gem install RedCloth -v '4.2.9'` succeeds before bundling.
错误

执行
gem install RedCloth -v '4.2.9'或
gem install RedCloth -v
单独安装RedCloth

若出现
ERROR:  Error installing RedCloth:
ERROR: Failed to build gem native extension.
Building has failed.
的错误

执行
xcode-select --install
重新安装xcode命令行工具

最后执行
rake install
完成

4、部署到github

需要配置SSH
在local目录查看是否有 cd ~/.ssh/id_rsa.pub
若有先备份
然后执行
ssh-keygen -t rsa -C “username@mail.com”
生成key

登陆github网站进入设置ssh keys

邮箱名称为title
id_rsa.pub内容为key

测试：ssh git@github.com
若出现
You’ve successfully authenticated, but GitHub does not provide shell access
Connection to github.com closed.
证明ssh登陆git通过

git config --global user.name "realname"
git config --global user.mail "username@mail.com"

至此ssh配置全部完成，下面开始发布网站到github上
rake setup_github_pages //配置github项目地址 接下来会提示输入url
rake generate  //本地生成
rake preview   //本地预览默认4000端口
rake deploy   //发布到github

访问 _config.yml文件中生成的url后面的地址可以查看最终效果
最后将source文件内容提交的github用来保存源码，便于以后写博客
