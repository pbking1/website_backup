---
layout: post
title: "IOS tutorial 1"
date: 2014-05-14 13:11:01 +0800
comments: true
categories: IOS
---
- 1.一点基本语法
- 用NSLog打印，代替printf（也是可以用的）
- 用NSDate来获取时间
- 用NSData来把数据char*转成string存起来
<!--more-->
- 源码
```
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[])
{

    @autoreleasepool {
        
        // insert code here...
        NSLog(@"Hello, World!");
        
    }
    int i;
    for(i = 0; i <= 5; i++)
        NSLog(@"%d\n", i);
   
    NSDate *yesterday = [NSDate dateWithTimeIntervalSinceNow:-(24*60*60)];
    NSLog(@"yesterday is %@", yesterday);
    
    NSDate *tomorrow = [NSDate dateWithTimeIntervalSinceNow:+(24*60*60)];
    NSLog(@"tomorrow is %@", tomorrow);
    
    const char *string = "Hi this is pb";
    NSData *data = [NSData dataWithBytes:string length:strlen(string) + 1];
    NSLog(@"data is %@", data);
    NSLog(@"%lu Bytes string is '%s'", (unsigned long)[data length], [data bytes]);
    return 0;
}
```

- 2.线程的同步与锁
　　- 要说明线程的同步与锁，最好的例子可能就是多个窗口同时售票的售票系统了。我们知道在java中，使用synchronized来同步，而iphone虽然没有提供类似java下的synchronized关键字，但提供了NSCondition对象接口。
	- 查看NSCondition的接口说明可以看出，NSCondition是iphone下的锁对象，所以我们可以使用NSCondition实现iphone中的线程安全。这是来源于网上的一个例子：

- 2.多个窗口同时售票的售票系统代码
- AppDelegate.h

```
#import <Cocoa/Cocoa.h>

@interface AppDelegate : NSObject <NSApplicationDelegate>{
    int tickets;
    int count;
    NSThread *ticketThreadone;
    NSThread *ticketThreadtwo;
    NSCondition *ticketsCondition;
    NSWindow *windows;
    
}

@property (assign) IBOutlet NSWindow *window;

@end

```

-  AppDelegate.cpp

```
#import "AppDelegate.h"

@implementation AppDelegate
@synthesize window;

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification
{
    tickets = 100;
    count = 0;
    
    ticketsCondition = [[NSCondition alloc] init]; //初始化锁对象
    ticketThreadone = [[NSThread alloc] initWithTarget:self selector:@selector(run) object:nil]; //初始化线程1
    [ticketThreadone setName:@"Thread-1"];
    [ticketThreadone start];
    
    ticketThreadtwo = [[NSThread alloc] initWithTarget:self selector:@selector(run) object:nil];  //初始化线程2
    [ticketThreadtwo setName:@"Thread-2"];
    [ticketThreadtwo start];
    
    [window makeKeyWindow];  //出错了，无法在窗口中运行，只能在命令行中运行，不知道为什么？求知道的筒子解答下~
    
}

- (void)run{
    while(TRUE){
        [ticketsCondition lock];
        if(tickets > 0)
        {
            [NSThread sleepForTimeInterval:0.5];
            count = 100 - tickets;
            NSLog(@"current tickets count are: %d, sell %d, thread name: %@", tickets, count, [[NSThread currentThread] name]);
            tickets--;
        }else
        {
            break;
        }
        [ticketsCondition unlock];
    }
}

- (void)dealloc{
    [ticketThreadone release];  //释放内存
    [ticketThreadtwo release];
    [ticketsCondition release];
    [window release];
    [super dealloc];
}



@end

```

- Trouble shooting
- 1.ARC forbids explicit message send of 'release'
'release' is unavailable: not available in automatic reference counting mode
	- 错误原因：因为我们设置了用ARC来管理内存释放，我们却又调用了release方法去释放对象。
	- (From the Internet)
		- ARC是iOS 5推出的新功能，全称叫 ARC(Automatic Reference Counting)。简单地说，就是代码中自动加入了retain/release，原先需要手动添加的用来处理内存管理的引用计数的代码可以自动地由编译器完成了。该机制在 iOS 5/ Mac OS X 10.7 开始导入，利用 Xcode4.2 可以使用该机制。简单地理解ARC，就是通过指定的语法，让编译器(LLVM 3.0)在编译代码时，自动生成实例的引用计数管理部分代码。有一点，ARC并不是GC，它只是一种代码静态分析（Static Analyzer）工具。
	- how to solve it?
		- 找到项目中的Build setting
			- 把`Objective-C Automatic Reference`从YES改成NO

- 2.找不到HOME键
    - 在模拟器上按`Shift+command+h`

- 3.出现`Auto Layout on iOS Versions prior to 6.0`
    - 界面设置问题
    - 找到storybroad
        - 打开属性栏，把`Use AutoLayout`去掉。

- 4.ios7的全屏问题
    - 在viewcontroller里面加入以下代码
    ```
    - (void)viewDidLayoutSubviews{
    
        if ([self respondsToSelector:@selector(topLayoutGuide)]) // iOS 7 or above
        {
            CGFloat top = self.topLayoutGuide.length;
            if(self.view.frame.origin.y == 0){
                // We only want to do this once, or if the view has somehow been &quot;restored&quot; by other code.
                self.view.frame = CGRectMake(self.view.frame.origin.x, self.view.frame.origin.y + top, self.view.frame.size.width, self.view.frame.size.    height - top);
            } 
        } 
    }
    ```
    - 这个只能让上面原有的时间什么的消失，但是从根本上不能解决问题

- 5.如果刚开始打开ios模拟器发现太大了
    - 再Window->scale那里可以调整成75%就可以使得模拟器看起来大小比较科学了。
