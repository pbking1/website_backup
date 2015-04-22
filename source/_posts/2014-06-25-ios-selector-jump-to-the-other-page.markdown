---
layout: post
title: "IOS selector(jump to the other page)"
date: 2014-06-25 11:02:32 +0800
comments: true
categories: IOS
---

###响应事件或者跳转
- 使用每个控件里面的action的selector
<!--more-->
```
UIBarButtonItem *leftbutton = [[UIBarButtonItem alloc] initWithTitle:@"cancel" style:UIBarButtonSystemItemDone target:self action:@selector(goBack)];
```

- 实现selector的跳转
	- 定义要跳转到的页面的viewcontroller
	- 用presentModalViewController跳转
	- 用完记得释放资源

```
- (void)goBack{
    basicinfo *p1 = [[basicinfo alloc] init];
    [self presentModalViewController:p1 animated:YES];
    [p1 release];
}
```