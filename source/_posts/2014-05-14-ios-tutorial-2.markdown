---
layout: post
title: "IOS tutorial 2"
date: 2014-05-14 16:34:49 +0800
comments: true
categories: IOS
---

- 键盘收起以及弹出对话框
- 在`ViewController.h`里面加入`-(IBAction)View_TouchDown:(id)sender`;
<!--more-->
```
#import <UIKit/UIKit.h>

@interface ViewController : UIViewController

@property (strong, nonatomic) IBOutlet UITextField *tempText;

-(IBAction)showMessage;
-(IBAction)View_TouchDown:(id)sender;
@end

```
- 在`ViewController.m`里面加入以下代码
```
- (IBAction)View_TouchDown:(id)sender
{
    [[UIApplication sharedApplication] sendAction:@selector(resignFirstResponder) to:nil from:nil forEvent:nil];
}

```

- 得到的全部代码如下

```
#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

- (void)viewDidLoad
{
    [super viewDidLoad];
	// Do any additional setup after loading the view, typically from a nib.
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

- (IBAction)showMessage  //弹出对话框
{
    UIAlertView *a = [[UIAlertView alloc]
                      initWithTitle:@"I am pb" message:@"hello world" delegate:nil cancelButtonTitle:@"I can do it" otherButtonTitles: nil];
    [a show];
}

- (IBAction)View_TouchDown:(id)sender
{
    [[UIApplication sharedApplication] sendAction:@selector(resignFirstResponder) to:nil from:nil forEvent:nil];
}

@end

```

- 最后再在storybroad里面用outlet把整个屏幕和`View_TouchDown`连接起来就可以了

- Touble shoot

	- 1.出现`'NSInternalInconsistencyException', reason: 'Could not load NIB in bundle:`
		- 说明`self.viewController = [[[ViewController alloc] initWithNibName:@"name" bundle:nil] autorelease];`
			- 里面的name写错了
				- 要写成和ViewController一样的名字才行。