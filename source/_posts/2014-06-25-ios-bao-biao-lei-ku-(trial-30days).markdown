---
layout: post
title: "IOS 报表类库（trial 30days）"
date: 2014-06-25 16:25:40 +0800
comments: true
categories: IOS
---

###一个非常容易使用的报表类库
- NChart3D
	- 但是只能免费使用30天
    - 并且经过真机调试
        - 效果做得很好，除了不能点击某个地方显示具体信息之外其他都做得很好
        - 比如可以方法缩小，左右拖，平移旋转都行
<!--more-->
- 在AppDelegate.m里面添加如下
```
#import "AppDelegate.h"
#import "NChart3D/NChart3D.h"
#import "ViewController.h"

@implementation AppDelegate
{
    UIWindow *m_window;
}
@synthesize window = m_window;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    m_window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    m_window.userInteractionEnabled = YES;
    m_window.multipleTouchEnabled = YES;
    [m_window makeKeyAndVisible];
    m_window.rootViewController = [[ViewController new] autorelease];
    // Override point for customization after application launch.
    return YES;
}
```

- 在Viewcontroller.h里面添加如下

```
#import <UIKit/UIKit.h>
#import "NChart3D/NChart3D.h"

@interface ViewController : UIViewController<NChartSeriesDataSource>

@end
```

- 在Viewcontroller.m里面添加如下

```
#import "ViewController.h"
#import "NChart3D/NChart3D.h"

@interface ViewController ()

@end

@implementation ViewController
{
    NChartView *m_view;
}

- (void)dealloc
{
    [m_view release];
    [super dealloc];
}

- (void)viewDidLoad
{
    [super viewDidLoad];
	// Do any additional setup after loading the view, typically from a nib.
    m_view = [[NChartView alloc] initWithFrame:CGRectZero];
    m_view.chart.licenseKey = @"";
    m_view.chart.cartesianSystem.margin = NChartMarginMake(10.0f, 10.0f, 10.0f, 20.0f);
    m_view.chart.shouldAntialias = YES;
    NChartColumnSeries *serires = [[NChartColumnSeries new] autorelease];
    serires.brush = [NChartSolidColorBrush solidColorBrushWithColor:[UIColor colorWithRed:0.0 green:0.7 blue:0.4 alpha:1.0]];
    serires.dataSource = self;
    [m_view.chart addSeries:serires];
    [m_view.chart updateData];
    self.view = m_view;   //使用新建的view
}

- (NSArray *)seriesDataSourcePointsForSeries:(NChartSeries *)series
{
    NSMutableArray *result = [NSMutableArray array];
    for(int i = 0; i < 10; i++)
        [result addObject:[NChartPoint pointWithState:[NChartPointState pointStateAlignedToXWithX:i Y:(rand()%30) + 1]forSeries:series]];
    return result;
}

- (NSString *)seriesDataSourceNameForSeries:(NChartSeries *)series
{
    return @"My series";
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end

```
- 效果
	- <img src="/images/ios/ios_table1.png">
