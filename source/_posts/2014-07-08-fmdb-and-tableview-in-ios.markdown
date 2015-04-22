---
layout: post
title: "FMDB and tableview in IOS"
date: 2014-07-08 16:01:33 +0800
comments: true
categories: 
---

###What is FMDB?
- FMDB is a framework that used to simplified the sqlite3 operation
- and we can use this framework to operate the sqlite easily
- and we need to download the fmdb package in github
	- then copy the fmdb folder to our project
	- include the sqlite3 framework in your project
- then you only need to write `import"FMDB.h"`
	- you will be able to use the api of fmdb
<!--more-->
###tableview is one of the most important thing in IOS
- just like the listview in android
- and the line in the tableview is called cell


###source code
- in the source code 
	- we do not use storybroad or xib
	- we just draw the things on the view
- Viewcontroller.h
```
#import <UIKit/UIKit.h>

@interface ViewController : UIViewController<UITableViewDataSource, UITableViewDelegate>{
    
}

@property NSInteger tag;

@end

```

- Viewcontroller.m
```
#import "ViewController.h"
#import "FMDB.h"
#import "detailViewController.h"

@interface ViewController ()

@end

@implementation ViewController
NSMutableArray *listofname;
@synthesize tag;

- (void)viewDidLoad
{
    [super viewDidLoad];
	listofname = [[NSMutableArray alloc]init];
    UITableView *tableview = [[UITableView alloc] initWithFrame:CGRectMake(0, 0, 320, 600)];
    
    //used to define the database 
    NSString *docdir = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
    NSString *dbpath = [docdir stringByAppendingPathComponent:@"db1.sqlite"];
    FMDatabase *db = [FMDatabase databaseWithPath:dbpath];
    [db open];
    //open the database
    if(![db open]){
        NSLog(@"could not open db");
    }
    //drop the table everytime because if you do not do this
    //the insert sentense will happen every time
    [db executeUpdate:@"drop table exercise"];
    [db executeUpdate:@"drop table poetries"];
    [db executeUpdate:@"create table exercise(_id integer, content text, answer text)"];
    [db executeUpdate:@"create table poetries(_id integer, title text, author text, age text, size integer, line1 text, line2 text, line3 text, line4 text, explain text)"];
    [db executeUpdate:@"insert into poetries(_id,title,author,age,size,line1,line2,line3,line4,explain) values(1,'赋得古原草送别','白居易','唐','5','离离原上草','一岁一枯荣','野火烧不尽','春风吹又生','译文：茂盛的野草长在古原上的野草多么茂盛，每年枯萎又每年新生。熊熊野火不能将它烧尽，春风吹过它又重获生命。')"];
    [db executeUpdate:@"insert into poetries(_id,title,author,age,size,line1,line2,line3,line4,explain) values(2,'春夜喜雨','杜甫','唐','5','好雨知时节','当春乃发生','随风潜入夜','润物细无声','译文：春雨知道适应季节，当万物萌发生长时，它伴随着春风，在夜晚偷偷地及时降临，滋润万物又细微无声。') "];
    [db executeUpdate:@"insert into poetries(_id,title,author,age,size,line1,line2,line3,line4,explain) values(3,'悯农','李绅','唐','5','锄禾日当午','汗滴禾下土','谁知盘中餐','粒粒皆辛苦','译文：这首悯农诗，写出了农民劳动的艰辛和对浪费粮食的愤慨。在盛夏的正午，农民顶着火辣辣的太阳锄地，汗水淼淌滴在庄稼地里。可是谁又知道，碗中的每一粒饭都包含着农民的辛苦啊!' )"];
    [db executeUpdate:@"insert into poetries(_id,title,author,age,size,line1,line2,line3,line4,explain) values(4,'静夜思','李白','唐','5','床前明月光','疑是地上霜','举头望明月','低头思故乡','译文：那透过窗户映照在床前的月光，起初以为是一层层的白霜。仰首看那空中的一轮明月，不由得低下头来沉思，愈加想念自己的故乡。')"];

    //query the database
    FMResultSet *rs = [db executeQuery:@"select * from poetries"];
    while ([rs next]) {
    	//add the title column in to the source of the table view
        [listofname addObject:[rs stringForColumn:@"title"]];
    }
    [db close];
    
    [tableview setDelegate:self];   //add the source and delegate
    [tableview setDataSource:self];
    [self.view addSubview:tableview];
}

//define the action in the cell 
- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    static NSString *cellidentifier = @"name";  
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:cellidentifier];
    
    if(cell == nil){
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:cellidentifier];
    }
    NSString *cellvalue = [listofname objectAtIndex:indexPath.row];
    cell.textLabel.text = cellvalue;
    cell.accessoryType = UITableViewCellAccessoryDisclosureIndicator;
    
    cell.userInteractionEnabled = YES;
    
    return cell;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
{
    return [listofname count];    //define the number of the row in tableview
}

- (NSInteger)tableView:(UITableView *)tableView indentationLevelForRowAtIndexPath:(NSIndexPath *)indexPath
{
    return 0;   //define the indent
}

//define the event when click the cell(very important)
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
    int mark = indexPath.row;  //pass the row number to the next controller using tag
    detailViewController *dv = [[detailViewController alloc] init];
    dv.tag = mark;
    [self presentModalViewController:dv animated:YES];
}

- (void)dealloc
{
    [listofname dealloc];
    [super dealloc];
}

- (void)viewDidUnload
{
    [super viewDidUnload];
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end

```

- detailViewController.h
```
#import <UIKit/UIKit.h>

@interface detailViewController : UIViewController

@property NSInteger tag;
@property UILabel *label;
@property UILabel *line1label;
@property UILabel *line2label;
@property UILabel *line3label;
@property UILabel *line4label;

@end

```

- detailViewController.m
```
#import "detailViewController.h"
#import "FMDB.h"
@interface detailViewController ()

@end

@implementation detailViewController

@synthesize tag;
@synthesize label;
@synthesize line1label;
@synthesize line2label;
@synthesize line3label;
@synthesize line4label;
NSMutableArray *listofname;

- (id)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil
{
    self = [super initWithNibName:nibNameOrNil bundle:nibBundleOrNil];
    if (self) {
        // Custom initialization
    }
    return self;
}

- (void)viewDidLoad
{
    self.view.backgroundColor = [UIColor whiteColor];
    NSString *tmep = [NSString stringWithFormat:@"%d", self.tag + 1]; 
    //convert the integer tag into string

    NSString *docdir = [NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES) lastObject];
    NSString *dbpath = [docdir stringByAppendingPathComponent:@"db1.sqlite"];
    FMDatabase *db = [FMDatabase databaseWithPath:dbpath];
    [db open];
    if(![db open]){
        NSLog(@"could not open db");
    }
    //use the tag passed by the previous controller and query the database
    FMResultSet *rs = [db executeQuery:@"select * from poetries where _id = ?", tmep];
    
    line1label = [[UILabel alloc] initWithFrame:CGRectMake(10, 10, 300, 20)];
    line2label = [[UILabel alloc] initWithFrame:CGRectMake(10, 50, 300, 20)];
    line3label = [[UILabel alloc] initWithFrame:CGRectMake(10, 80, 300, 20)];
    line4label = [[UILabel alloc] initWithFrame:CGRectMake(10, 100, 300, 20)];
    while ([rs next]) {
        line1label.text = [rs stringForColumn:@"line1"];
        line2label.text = [rs stringForColumn:@"line2"];
        line3label.text = [rs stringForColumn:@"line3"];
        line4label.text = [rs stringForColumn:@"line4"];
    }
    [self.view addSubview:line1label];
    [self.view addSubview:line2label];
    [self.view addSubview:line3label];
    [self.view addSubview:line4label];
    [db close];
    [super viewDidLoad];
	// Do any additional setup after loading the view.
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end

```