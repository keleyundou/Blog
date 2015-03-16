---
layout: post
title: "iOS系统兼容性需求的方法"
date: 2015-03-16 14:38:45 +0800
comments: true
categories: New
description: "iOS系统兼容性需求的方法" 
keywords: iOS系统兼容

---
####iOS系统兼容性需求的方法

·判断系统版本，按运行时的版本号运行代码


``` 
// System Versioning Preprocessor Macros
#define SYSTEM_VERSION_EQUAL_TO(v) ([[[UIDevice currentDevice] systemVersion] compare:v options:NSNumericSearch] == NSOrderedSame)
#define SYSTEM_VERSION_GREATER_THAN(v) ([[[UIDevice currentDevice] systemVersion] compare:v options:NSNumericSearch] == NSOrderedDescending)
#define SYSTEM_VERSION_GREATER_THAN_OR_EQUAL_TO(v) ([[[UIDevice currentDevice] systemVersion] compare:v options:NSNumericSearch] != NSOrderedAscending)
#define SYSTEM_VERSION_LESS_THAN(v) ([[[UIDevice currentDevice] systemVersion] compare:v options:NSNumericSearch] == NSOrderedAscending)
#define SYSTEM_VERSION_LESS_THAN_OR_EQUAL_TO(v) ([[[UIDevice currentDevice] systemVersion] compare:v options:NSNumericSearch] != NSOrderedDescending)
```

```
使用:
if (SYSTEMVERSIONLESS_THAN(@“5.0”)) 
{ 
	//系统版本小于5.0...
	Do something... 
} 

```