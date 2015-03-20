---
layout: post
title: "Storyboard中TabBar显示灰色外观的问题"
date: 2015-03-18 12:54:01 +0800
comments: true
categories: New
description: "Storyboard中TabBarr显示灰色外观的问题"
keywords: TabBar

---
<p>现象：</p>
<p>tabbar上的图片不是预期的图标，而是呈现出一个该图标的灰色形状，一眼看上去不是让人舒服。</p>

![这里写图片描述](http://img.blog.csdn.net/20150317152916295)

<p>原因：</p>
tabbar上的图片本质上不是一个图片，而是一个形状图片。系统对我们使用的图片也只是把其中的形状"扣"出来，其余的背景什么的都不要。因为我们可能给背景加了颜色，所以系统扣的时候只是把背景扣出来了，我们模拟时只看到一个方块，而且还是系统处理过成灰色。

<!--more-->

<p>解决办法：</p>
<p>如图，选中Original Image，OK！</p>
<p>或者让UI将染色淡化为透明最好</p>
![这里写图片描述](http://img.blog.csdn.net/20150317153030038)
<p>效果图如下</p>

<p>用Storyboard设置Tab Bar Controller 的item选中方法</p>
[Setting Selected Image in Tab Bar Controller with Storyboard](http://stackoverflow.com/questions/21386101/setting-selected-image-in-tab-bar-controller-with-storyboard) 链接
<p>首先进入Storyboard，选中TabBarItem，选择Show the Identity inspector ，在Runtime Attributes中的Keypath栏添加'selectedImage'，Type选择'Image'， value栏填写 'your_image_name'(你图片的名字)</p>
<p>如图</p>
![](http://img.blog.csdn.net/20150317173619941)