---
layout: post
title: "Zst Internship IOS Code step2"
date: 2014-05-23 15:21:09 +0800
comments: true
categories: IOS Internship
---

###Here are the method added
- I want to implement a button that used to went back to the main page if the user suddenly do not want to continue ordering the things
	- First
		- Go to Sections -> ButtonMacro.h
			- add `#define BACKTOMAINPAGE 13` at the end
		- then go to Sections -> Buttons -> CreateButtom.m
			- add the following code
			
```
else if (_type == BACKTOMAINPAGE) 
{
    self.frame = CGRectMake(50, 50, 40, 44);
    [self setTitle:@"返回主页" forState:UIControlStateNormal];
    [self setTitle:@"返回主页" forState:UIControlStateHighlighted];
}

```

<!--more-->
- go to Controller -> 我 -> 应用推荐 -> OrderDetailViewController.m
	- and this is create a button on the right top corner and its function is to went back to the mainpage
	- add the following code in `viewdidload` function

```
	ButtonFactory *buttonFactory = [ButtonFactory factory];
    UIButton *rightBtn = [buttonFactory createButtonWithType:BACKTOMAINPAGE];
   	[rightBtn addTarget:self action:@selector(gobacktomain:) forControlEvents:UIControlEventTouchUpInside];
 	UIBarButtonItem *rightBarItem = [[UIBarButtonItem alloc] initWithCustomView:rightBtn];
 	self.navigationItem.rightBarButtonItem = rightBarItem;
  	[rightBarItem release];
```
- add a new function called `gobacktomain`
	- this is a selector that used to find the main viewcontroller and jump to it.
	- the code in it is

```
	- (void)gobacktomain:(id)paramSender{
	    UIViewController *target = nil;
    	for(UIViewController *controller in self.navigationController.viewControllers){
        	if([controller isKindOfClass:[HomePageViewController class]]){
   				target = controller;
       		}
    	}
    	if(target){
        	[self.navigationController popToViewController:target animated:YES];
    	}
	}
```
