---
layout: post
title: "IOS UIButton"
date: 2014-06-25 11:01:58 +0800
comments: true
categories: IOS
---

###IOS的button其实和其他的控件使用方法差不多
- 首先初始化button，用CGRectMake把控件画在view上
- 使用setTitle设置button的文字
- 使用layer来设置边界
- 用action里面设置selector来跳转或者响应事件
<!--more-->

```
    UIButton *button1 = [[UIButton alloc] initWithFrame:CGRectMake(0, 420, 160, 44)];
    [button1 setTitle:@"进度填报" forState:UIControlStateNormal];
    //button1.backgroundColor = [UIColor colorWithRed:(12/255) green:(22/255) blue:(32/355) alpha:1.0];
    [button1.layer setBorderWidth:1.0];
    [button1 setTitleColor:[UIColor lightGrayColor] forState:UIControlStateNormal];
    [button1 addTarget:self action:@selector(gotorenewpage:) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button1];
```

```
- (void)gotorenewpage:(UIButton *)paramSender{
    viewcontroller *p = [[viewcontroller alloc] init];
    [self presentModalViewController:p animated:YES];
    [p release];
}
```