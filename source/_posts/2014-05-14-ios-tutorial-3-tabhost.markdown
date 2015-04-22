---
layout: post
title: "IOS tutorial 3 tabhost"
date: 2014-05-14 21:25:25 +0800
comments: true
categories: IOS
---

###源代码
- 把数据载入到tableview中，，点击某一个item就可以出发alert对话框。
- Cell 的样式也是可以自定义的
	- 通过UITableViewCell来设置样式
- 在`AppDelegate.h`中
- 加入mainView的声明
	- **注意要加`#import "ViewController.h"`**
<!--more-->
```
#import <UIKit/UIKit.h>
#import "ViewController.h"

@interface AppDelegate : UIResponder <UIApplicationDelegate>

@property (strong, nonatomic) UIWindow *window;
@property (strong, nonatomic) ViewController *mainView;

@end
```
- 在`AppDelegate.m`中加入以下代码

```
- (void)dealloc
{
    [_window release];
    [_mainView release];
    [super dealloc];
}

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    self.window = [[[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]] autorelease];
    self.mainView = [[[ViewController alloc] init] autorelease];
    
    self.window.rootViewController = self.mainView;
    [self.window makeKeyAndVisible];
    // Override point for customization after application launch.
    return YES;
}
```
- 修改`ViewController.h`

```
#import <UIKit/UIKit.h>

@interface ViewController : UIViewController<UITableViewDataSource, UITableViewDelegate>

@property (nonatomic, retain) NSMutableArray *datalist;
@property (nonatomic, retain) UITableView *myTableView;

@end

```

- 文件`ViewController.m`如下

```
#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController
@synthesize datalist;
@synthesize myTableView;

- (void)viewDidLoad
{
    [super viewDidLoad];
	// Do any additional setup after loading the view, typically from a nib.
    NSMutableArray *list = [NSArray arrayWithObjects:@"武汉",@"上海",@"北京",@"深圳",@"广州",@"重庆",@"香港",@"台海",@"天津", nil];
    self.datalist = list;
    
    UITableView *tableview = [[[UITableView alloc] initWithFrame:self.view.frame style:UITableViewStylePlain] autorelease];
    //set the data source
    tableview.dataSource = self;
    //set the delegate
    tableview.delegate = self;
    //set the background
    //tableview.backgroundView = [[UIImageView alloc] initWithImage:[UIImage imageNamed:@"Background.png"]];
    self.myTableView = tableview;
    [self.view addSubview:myTableView];
    
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *CellWithIdentifier = @"Cell";
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:CellWithIdentifier];
    if(cell == nil){
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleValue2 reuseIdentifier:CellWithIdentifier];
    }
    NSUInteger row = [indexPath row];
    cell.textLabel.text = [self.datalist objectAtIndex:row];
    return cell;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
{
    return [self.datalist count];
}

- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath
{
    return 70;  //设置行高
}

- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
    NSString *msg = [[NSString alloc] initWithFormat:@"You choose :%@",  [self.datalist objectAtIndex:[indexPath row]]];
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Alert" message:msg delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil];
    [msg release];
    [alert show];
}

- (void)tableView:(UITableView *)tableView commitEditingStyle:(UITableViewCellEditingStyle)editingStyle forRowAtIndexPath:(NSIndexPath *)indexPath
{
    NSLog(@"delete");  //滑动删除
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end
```