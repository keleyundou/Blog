---
layout: post
title: "基于Octopress和github搭建个人博客的过程"
date: 2015-03-13 12:16:14 +0800
comments: true
categories: New
description: "基于Octopress和github搭建个人博客的过程"
keywords: Octopress

---
   促使我搭建个人博客的原因应该归结于那些大牛们都有属于自己的博客站点，感觉挺牛X的；另一方面就是想有个干净整洁的纯技术博客。
   
   下面分享下我是怎么搭建此博客的。
   
####首先安装ruby
   
   http://octopress.org/docs/setup/
   
```
brew update
brew install rbenv
brew install ruby-build

rbenv install 1.9.3-p0
rbenv local 1.9.3-p0
rbenv rehash
```
   你有可能需要安装老版本的GCC编译器才能顺利安装Ruby 1.9.3:
   
```
brew tap homebrew/dupes
brew install apple-gcc42
```
<!--more-->

####安装Octopress
先从git上将octopress clone下来：

```
git clone git://github.com/imathis/octopress.git Octopress
cd Octopress
```
####然后安装依赖：
进入Octopress目录，执行如下命令：

```
gem install bundler
rbenv rehash
bundle install
```
####最后安装Octopress

进入Octopress目录，执行如下命令：

```
rake install
```
####发布Octopress到Github
进入Octopress目录，执行如下命令：

```
rake setup_github_pages
```
在Repository url中输入刚刚创建的仓库地址：git@github.com:username/username.github.io.git，自行替换username。

然后生成静态页面发布

```
rake generate
rake deploy
```
提交源文件，即source分支

```
git add .
git commit -m 'your message'
git push origin source
```

####博文的发表
进入Octopress目录，执行如下命令：

生成博文框架，然后修改生成的文件即可

```
rake new_post["title"]
# Creates source/_posts/2011-07-03-title.markdown
```

生成静态文件和在本机4000端口生成访问内容

```
rake generate && rake preview
```

发布文件

```
rake deploy
```







参考：

·http://blog.devtang.com/blog/2012/02/10/setup-blog-based-on-github/

·http://blog.csdn.net/jackystudio/article/details/16117585