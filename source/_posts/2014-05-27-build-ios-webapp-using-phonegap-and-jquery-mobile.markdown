---
layout: post
title: "build ios webapp using phonegap and jquery mobile"
date: 2014-05-27 17:30:09 +0800
comments: true
categories: html IOS
---

###first install phonegap
- download `phonegap-2.9.1`
	- enter the lib/ios/bin
	- use the command `./create ~/Documents/html_app/testphonegap test_phonegap test1`
		- to create the project that is located in `~/Documents/html_app/` and the name of it is `test_phonegap`
<!--more-->
###then use xcode to open the project
- add the following code in the index.html and run the simulater
- the jquery mobile is used from internet and we do not need to download it
	- but I can not find out a way to use the jquery mobile js file in my computer
- remember to add `<meta http-equiv="Content-Type" content="text/html; charset=utf-8">` to enable the chinese utf-8

```
<html>
    <head>
        <link rel="stylesheet" href="http://code.jquery.com/mobile/1.3.2/jquery.mobile-1.3.2.min.css">
            <script src="http://code.jquery.com/jquery-1.8.3.min.js"></script>
            <script src="http://code.jquery.com/mobile/1.3.2/jquery.mobile-1.3.2.min.js"></script>
             <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    </head>
    <body>
        <div data-role="page" id="pageone">
            <div data-role="header">
                <h1>欢迎来到我的主页</h1>
                <div data-role="navbar">
                    <ul>
                        <li><a href="#" class="ui-btn-active" data-icon="home">首页</a></li>
                        <li><a href="#pagetwo" data-icon="arrow-r">页面二</a></li>
                    </ul>
                </div>
                <select name="day" id="day">
                    <optgroup label="Weekdays">
                        <option value="mon">Monday</option>
                        <option value="tue">Tuesday</option>
                        <option value="wed">Wednesday</option>
                    </optgroup>
                    <optgroup label="Weekends">
                        <option value="sat">Saturday</option>
                        <option value="sun">Sunday</option>
                    </optgroup>
                </select>
            </div>
            
            <div data-role="content">
                <p>本例设有 ui-btn-active 类，请注意首页按钮时突出显示的（已选）。</p>
                <p>如果点击页面二，您会注意到按钮不会突出显示。</p>
            </div>
            
            <div data-role="footer">
                <h1>我的页脚</h1>
            </div>
        </div>
        
        <div data-role="page" id="pagetwo">
            <div data-role="header">
                <h1>欢迎来到我的主页</h1>
                <div data-role="navbar">
                    <ul>
                        <li><a href="#pageone" data-icon="home">首页</a></li>
                        <li><a href="#" data-icon="arrow-r">页面二</a></li>
                    </ul>
                </div>
            </div>
            
            <div data-role="content">
                <p>本页中没有被预选的按钮（突出显示）。</p> 
                <p>如需让按钮被选的外观表示当前正在访问页面，请返回导航栏教程，继续向下阅读。</p>
            </div>
            
            <div data-role="footer">
                <h1>我的页脚</h1>
            </div>
        </div> 
    </body>
</html>

``` 