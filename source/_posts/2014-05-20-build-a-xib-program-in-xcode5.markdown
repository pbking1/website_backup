---
layout: post
title: "build a xib program in xcode5"
date: 2014-05-20 19:45:48 +0800
comments: true
categories: IOS
---

- 由于xcode5里面默认使用了storyboard这种视图控制器，因此有以下的解决方案
	- 1.新建工程--ios---Application---Single View Application
	- 2.将自动生成的Main.storyboard,ViewController.h,ViewController.m这三个文件彻底删除
	- 3.在项目设置里面,将MainInterface这一项中的内容删除置为空
	- 4.新建一个类,继承UIViewController,并且选中WithXIB for user interface.并且把内存计数器改为MRC.(改成MRC的方法就是再build setting里面找automatic, 然后把Object-C Automatic Reference Counting改成NO)
	<!--more-->
	- 5.在AppDelegate中,导入新建的类:ViewController.h
	- 6.在AppDelegate.h中,添加属性:@property(strong,nonatomic)ViewController*viewController;
	- 7.在AppDelegate.m中,添加以下代码:
```
	self.window= [[[UIWindowalloc]initWithFrame:[[UIScreenmainScreen]bounds]]autorelease];
	self.viewController= [[[PT4ViewControlleralloc]initWithNibName:@"PT4ViewController"bundle:nil]autorelease];
	self.window.rootViewController=self.viewController;
	[self.windowmakeKeyAndVisible];
```
	- 8.处理好内存分配以及dealloc方法.
```
	- (void)dealloc
	{
		[_window release];
		[_viewController release];
		[super dealloc];
	}
```