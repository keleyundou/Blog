---
layout: post
title: "多台电脑写博客之博客克隆"
date: 2015-04-01 18:23:10 +0800
comments: true
categories: New
description: "多台电脑写博客之博客克隆"
keywords: 博客克隆
---
####创建一个本地的Octopress仓库
重新创建一个本地的Octopress仓库只需执行以下几步骤即可。
#####拉取Octopress仓库内容
首先克隆自己的Octopress仓库，初始化git仓库，添加远程仓库，也就是你自己的Octopress地址，pull到远程仓库。在终端执行如下命令：

```
mkdir Octopress
cd Octopress
git init
git remote add origin git@github.com:username/username.github.com.git
git pull origin
```
<!--more-->

#####切换到source分支
这时候进入Octopress目录，发现除了初始化生成的.git目录外什么都没有。执行如下命令后source分支的东西就都出来的了。

```
git checkout source
```
#####建立github pages
```
rake setup_github_pages
```
#####拉取master分支
进入_deploy目录，运行如下命令：

```
git pull origin master
```
#####切换回source分支
```
git checkout source
```
至此，Octopress就在另一台电脑上克隆好了，你就可以在不同的电脑上维护同一个博客了，运行一下如下命令，确认没有问题。

```
rake generate
rake preview
rake deploy
```
#####更新和推送
当你要在一台电脑上写博客或更改时，首先更新source仓库。更新master并不是必须的，因为你更改源文件之后还是需要rake generate的。

```
cd Octopress
git pull origin source
cd _deploy
git pull origin master
```
写完博客之后不要忘了推送到remote，下面的命令在每次处理完博客事务后记得要运行。

```
rake generate
git add .
git commit –m "commit message"
git push origin source
rake deploy
```

#####遇到的问题
当你换了一台新电脑之后，需要重新签名，签名请参考[generating-ssh-keys](http://https://help.github.com/articles/generating-ssh-keys/)
