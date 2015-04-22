---
layout: post
title: "IOS UILabel and UITextfield"
date: 2014-06-25 15:00:33 +0800
comments: true
categories: IOS
---

###label
- 相当于android里面的textview
- 用setText来设置内容
- setBackground来设置背景颜色
<!--more-->
```
	UILabel *label1 = [[UILabel alloc] initWithFrame:CGRectMake(10, 60, 290, 44)];
    [label1 setText:@"项目里程碑                          请选择>"];
    [label1 setBackgroundColor:[UIColor whiteColor]];
    [self.view addSubview:label1];

```

###textfield
- 相当于android里面的edittext
- 用layer.cornerRadius设置圆角
- placeholder设置hint，提示
- 貌似使用这些方法需要把UITextfield定义在.h里面

```
	UITextField *text1 = [[UITextField alloc] initWithFrame:CGRectMake(10, 340, 290, 84)];
    self.text1.placeholder = @"进度说明";
    self.text1.layer.cornerRadius = 10;
    [text1 setBackgroundColor:[UIColor whiteColor]];
    [self.view addSubview:text1];
```
