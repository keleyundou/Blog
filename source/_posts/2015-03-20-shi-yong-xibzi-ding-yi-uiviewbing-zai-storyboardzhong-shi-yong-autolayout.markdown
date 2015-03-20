---
layout: post
title: "使用Xib自定义UIView并在Storyboard中使用AutoLayout"
date: 2015-03-20 21:47:56 +0800
comments: true
categories: New
description: "使用Xib自定义UIView并在Storyboard中使用AutoLayout"
keywords: Xib Storyboard

---

Xib和Storyboard的使用我就不多叙述。关于如何用Xib自定义一个UIView，并将其添加在ViewController上，使用AutoLayout添加约束条件，使其跟随控制器ViewController的约束条件变化而变化呢？请看下文。

 1、 创建一个继承UIView的子类TestView和xib文件
 
 <img src="http://img.blog.csdn.net/20150320213205724" alt width="640"/>
 
 2、 选中xib中的File's Owner，设置右边工具栏中的Custom Class为你所创建的文件TesView
 3、 在TestView.h中添加一个IBOutlet属性
 

```
@property (nonatomic, weak) IBOutlet UIView *view;
```
<!--more-->

 4、 将此IBOutlet 连接到TestView.xib 的View
 
<img src="http://img.blog.csdn.net/20150320213447559" alt width="640" height="200"/>

 5、在TestCustomView.m文件中初始化，如下：
 

```
- (instancetype)initWithCoder:(NSCoder *)aDecoder
{
    self = [super initWithCoder:aDecoder];
    if (self) {
        NSString *className = NSStringFromClass([self class]);
        self.view = [[[NSBundle mainBundle] loadNibNamed:className owner:self options:nil] firstObject];
        [self addSubview:self.view];
        return self;
    }
    return nil;
}

```

或者在awakeFromNib中添加也可以：


```
- (void)awakeFromNib {
    [[[NSBundle mainBundle] loadNibNamed:NSStringFromClass([self class]) owner:self options:nil] firstObject];
    [self addSubview:self.view];
}
```

6、在Storyboard中引用xib文件

<img src="http://img.blog.csdn.net/20150320213639439" alt width="640"/>





