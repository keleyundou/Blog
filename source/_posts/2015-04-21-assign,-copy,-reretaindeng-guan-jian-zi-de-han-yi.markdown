---
layout: post
title: "assign、copy、reretain等关键字的含义"
date: 2015-04-21 14:06:31 +0800
comments: true
categories: new
#下面为新增内容
description: "assign、copy、reretain等关键字的含义"
keywords: assign、copy、reretain

---

######前言

assign:简单赋值，不更改索引计数

copy:建立一个索引计数为1的对象，然后释放旧对象

retain:释放就对象，将旧对象的值赋予输入对象，再将输入对象的索引计数加1

copy 其实就是建立了一个相同的对象，而retain不是：

比如，一个NSString对象，地址为0x1111，内容为@"Hello，world！"；copy到另一个NSString对象之后，地址为0x2222，内容相同，新的对象retain为1，旧的对象索引计数没用变化。

retain到另一个NSString对象之后，地址相同（建立一个指针，指针拷贝），内容相同，这个对象的retain值+1

也就是说，retain是指针拷贝，而copy是内容拷贝。拷贝之前都会将旧的对象给释放掉。
<!--more-->
######使用范围：

*assign的使用：一般对应于基础数据类型（NSInteger）和C数据类型（int, float, double, char 等）

*copy的使用：一般对应于NSString

*retain的使用：一般对应于NSObject和其他子类

1.readonly：表示这个属性是只读的，就是只生成getter方法不会生成setter方法；

2.readwrite：设置可供访问级别；

3.retain：旨在说明该属性在赋值的时候，先release掉之前的值，然后再赋新值给属性，引用计数再+1；

4.nonatomic：非原子性访问，不加同步，多线程并发访问会提高性能。注意：如果不加此属性，则默认是两个访问方法都为原子型事务访问。


######区别

1.假设用malloc分配了一个块内存，并把它的地址赋值给了指针a，然后你希望指针b也共享这块内存，于是你又把a赋值给（assign）了b。至此a和b就指向了同一块内存，请问当a不再需要这块内存是，能否直接释放掉？答案为No！是的，因为a并不知道b是否还在使用这块内存，如果a释放了，那么b在使用这块内存的时候会引起程序crash。

2.了解到1中assign的问题后，那么问题来了，该如何解决呢？最简单的一个方法就是：使用引用计数。还是上面那个问题，我们给那块内存设一个内存引用计数，当内存被分配并且赋值给a时，引用计数是1。当a赋值给b时，引用计数增加到2，这时如果a不再使用这块内存，它只需把引用计数减1，表明自己不再拥有这块内存，b不再使用这块内存时也把引用计数减1，当引用计数变为0时，代表该内存不再被任何指针所引用，系统可以把它直接释放掉。

3.上面两点其实就是assign和retain的区别，assign就是直接赋值，从而会引起1中的问题。当数据为int, float,等原生类型时，可以使用assign。retain就如2中所述，使用了引用计数，retain引起引用计数+1，release引起引用计数-1，当引用计数为0时，dealloc函数将会被调用，内存被回收。

4.copy是在你不希望a和b共享同一块内存是使用到。a和b各自有各自的内存。

5.atomic 和 nonatomic用来决定编译器生成的getter和setter是否为原子操作。在多线程环境下，原子操作是必要的，否则有可能引起错误的结果。加了atomic后, setter函数会变成这样：

```
if (property != newValue) {
	[property release];
	property = [newValue retain];
}
```