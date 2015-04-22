---
layout: post
title: "IOS segment control"
date: 2014-06-25 11:01:49 +0800
comments: true
categories: IOS
---

###segment control
- 这一段是使用CGrectmake在view上直接按照坐标大小画segment control
- 因为tabbar只能按照默认的放在底部
- 因此要使用放在顶部的类似tabbar的效果有两种方式
	- 一种就是segment control，每点击一个item就跳转到那个item对应的view那里
	- 还有一种是使用button来仿造tabbar
	- 不过总体来说还是button效果好一点
<!--more-->
```
- (void)viewDidLoad
{
    [super viewDidLoad];
    //segment control
    NSArray *items = [NSArray arrayWithObjects:@"关注项目", @"全部项目", nil];
    UISegmentedControl *segmentedControl = [[UISegmentedControl alloc] initWithItems:items];
    [segmentedControl setFrame:CGRectMake(15, 50, 300, 50)];  //画segment control
    [segmentedControl addTarget:self action:@selector(segmentedControlChangedValue:) forControlEvents:UIControlEventValueChanged];  //响应事件
    [segmentedControl setTag:1];
    [self.view addSubview:segmentedControl];
    [segmentedControl release];

}
```

- 接下来通过使用不同的segmentControl里面的index来判断点了哪个，然后进行跳转

```
- (void)segmentedControlChangedValue:(UISegmentedControl *)segmentedControl {
    NSInteger selectedindex = [segmentedControl selectedSegmentIndex];
    if(selectedindex == 0){
        partViewController *p = [[partViewController alloc] init];
        [self presentModalViewController:p animated:YES];
        //[self dismissModalViewControllerAnimated:YES];
        [p release];
    }else if(selectedindex == 1){
        allproViewController *a = [[allproViewController alloc] init];
        [self presentModalViewController:a animated:YES];
        //[self dismissModalViewControllerAnimated:YES];
        [a release];
    }
}
```
