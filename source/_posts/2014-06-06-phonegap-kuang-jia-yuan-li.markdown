---
layout: post
title: "phonegap 框架原理"
date: 2014-06-06 17:03:43 +0800
comments: true
categories: System_analyze_and_design Android html
---

####phonegap 实现原理
- `关键`
	- 1.用webview在本地来渲染解析html
		- **因此实际上他就是一个内嵌的浏览器**
			- 类似于一个WebView，但是phonegap对webview做了些改造
	- 2.基于plugin模式来封装调用原生API
		- 以原生app的方式来运行
		- 用js调用原生的功能
	- 3.在框架首次启动的时候加载CallbackServer线程，并且监听前端XHR请求和链表中有无数据
		- 当XHR请求来了而链表为空，则线程等待10秒
			- 如果这个时间内有数据来，那么就唤醒线程把数据传到前端
		- 如果10s后没有数据，则传空数据回前端
		- `基于服务器推技术`
	- 4.同步请求和异步请求有关键的区别
<!--more-->
- `他如何实现跨平台的`
	- phonegap在每一种中都实现了一套后台的框架，分别和每个平台的API进行交互，从而调用它的原生API，然后对应开发人员提供统一的接口，也就是phonegap的API。
	- 因此，开发人员只需要使用web技术就可以对移动平台进行快速开发
	- 而且跨平台也是只是前端跨平台。
- `这个开源的项目的贡献者`
	- 这个开源项目中IBM贡献的代码比创始者（温哥华的一家小公司）还多。
	- Apache Cordova是phongap贡献给apache的一个开源项目
		- 他有phonegap里面的核心代码


####phonegap的优点
- app的前台兼容性好
- 标准化， 由于使用的是W3C标准，所以web前端可直接用于web app。
- js+html5和java+xml很像
- 装起来也不麻烦，用起来比较容易
- 提供硬件访问

####phonegap的缺点
- 反应很慢（亲身实践过）
- 交互很差
- 内存消耗大
	- 有人做过测试，和用java写android对比，phonegap明显消耗更多内存
	- 而且释放内存很慢
- 调试也麻烦

####有谁在用
- wikipedia
	- 它的移动应用就是用phonegap写的
- Facebook
	- 移动版SDK的一部分是cordova的一个分支
- Salesforce
	- 移动版的SDK的一部分是cordova的一个分支
- IBM
	- 移动平台建立在phonegap上
	- 并且积极参与到phonegap的开发里面
- Microsoft
	- 正在积极参与windows phone的那一部分的开发
- Adobe
	- 2011年Adobe收购了phonegap得私人开发商Notibi，并将phonegap贡献给apache并且开源
- blackberry
- zynga
	- 用phonegap和html5写了不少很好的游戏
- cisco


