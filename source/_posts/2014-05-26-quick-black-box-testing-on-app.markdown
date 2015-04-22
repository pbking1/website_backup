---
layout: post
title: "quick black box testing on app"
date: 2014-05-26 14:39:28 +0800
comments: true
categories: software_testing Android
--- 

###some quick black box testing tools
- calabash
- appium
- appgrader
- monkey(adb 自带)
<!--more-->
###and if you want to install app on the blue stack simulater
- use SnapPea_apk_installer
- http://mac.softpedia.com/dyn-postdownload.php?p=133201&t=0&i=1

###appium
- how to install
	- `brew install node`      # get node.js
	- `npm install -g appium ` # get appium
	- `npm install wd `        # get appium client
	- `appium & `              # start appium
	- `node your-appium-test.js`

###monkey
- Monkey测试是Android平台下自动化测试的一种快速有效的手段，通过Monkey工具可以模拟用户触摸屏幕、滑动轨迹球、按键等操作来对模拟器或者手机设备上的软件进行压力测试，检测该软件的稳定性、健壮性。它的原理是向系统发送伪随机的用户事件流（如按键输入、触摸输入、手势输入等），实现对正在开发的应用程序进行压力测试。

- Monkey的特性
   -（1）测试的对象仅为应用程序包（apk包），有一定的局限性；
   -（2）Monkey测试使用的事件流数据流是随机的，不能进行自定义；
   -（3）可对MonkeyTest的对象、事件数量、类型、频率等进行设置。

- Monkey测试的停止条件
	-（1）如果先顶了Monkey运行在一个或几个特定的包上，那么它会检测试图转到它包的操作，并对其进行阻止；
	-（2）如果应用程序崩溃或接收到任何失控异常，Monkey将停止并报错；
	-（3）如果应用程序产生了应用程序不响应（application not responding）的错误，Monkey将会停止并报错。
通过多次并且不同设定下的Monkey测试才算它是一个稳定性和健壮性足够的程序。

- 随着测试的深入，我们需要忽略App的崩溃（App的崩溃会导致Monkey测试的停止），而不是停住，monkey同样能做到。--ignore crashes
甚至，它还能生成profiling报告。 --hprof

- Monkey具体参数的设定可参考：
	- http://developer.android.com/tools/help/monkey.html

- 使用方法
	- 本方法基于mac上的bluestack模拟器
	- 1.首先打开bluestack模拟器，然后进行`adb connect localhost:10001`
	- 2.显示连接上了之后，使用SnapPea_APK_Installer安装需要测试的apk
	- 3.然后成功安装上之后。由于需要知道应用程序的主Activity，则用`adb shell`进入模拟器的系统，然后再`data/data`里面看名字，但是由于bluestack没有破解，所以权限不够，看不了
	- 4.因此，用命令`adb shell monkey 100`,让他随机测一下，然后看看报的主程序名字是什么。
		- adb shell monkey [options]
			- 如果不指定options，Monkey将以无反馈模式启动，并把事件任意发送到安装在目标环境中的全部包。下面是一个更为典型的命令行示例，它启动指定的应用程序，并向其发送1000个伪随机事件：
	- 5.再用`adb shell monkey -p com.baofood -v 1000000 -hprof`去测试
		- monkey -p（package的意思）  指定文件名 -v（测试的次数和频率） number（次数）







