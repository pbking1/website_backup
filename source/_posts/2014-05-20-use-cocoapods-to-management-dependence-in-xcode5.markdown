---
layout: post
title: "use CocoaPods to management dependence in xcode5"
date: 2014-05-20 20:05:22 +0800
comments: true
categories: IOS
---

###What is CocoaPods?
- CocoaPods is a tools used to management the Third party code in IOS project

###How to install it?
- use the ruby gem to install
	- `sudo gem install cocoapods`
	- and the ruby should be above ruby 2.0
	- `pod setup`
		- this step is download the info in the ~/.cocoapods
		- and you can use `du -sh *` to see how it process
	- if the gem is too old
		- use `sudo gem update --system`
<!--more-->
- most inportantly
	- for the ruby's software source is using the Amazon could and will be block by the great fire wall.
	- so you need to change to ruby temperatly
		
		```
		gem sources --remove https://rubygems.org/
		gem sources -a http://ruby.taobao.org/
		```
	- after that 
		- you can install the pod
- and when you need to use the pod
	- change back to the origin source

###how to use it?
- we will need a file called `Podfile`
	- and the content of it is 
```
platform :ios, '7.0'
pod 'Mantle'
pod 'LBBlurredImage'
pod 'TSMessages'
pod 'ReactiveCocoa'
```
	- then press `ctrl + O` and rename into `Podfile`
	- press `ctrl + x` to exit 
- after that
	- use `pod install`
		- and you will see
```
$ pod install
Analyzing dependencies
CocoaPods 0.28.0 is available.
Downloading dependencies
Installing HexColors (2.2.1)
Installing LBBlurredImage (0.1.0)
Installing Mantle (1.3.1)
Installing ReactiveCocoa (2.1.7)
Installing TSMessages (0.9.4)
Generating Pods project
Integrating client project
[!] From now on use `SimpleWeather.xcworkspace`.
```

- and the Cocoapods will create a xxxxx.xcworkspce

###Something else
- after you use `pod install`
	- a file called `Podfile.lock` will be generated and this file should not be add into the .gitignore.
	- for this file will lock on all the version of the dependences
	- and you will not be able to change the version of these dependences even you use `pod install`
	- and only the command `pod update` will work.

###generate the doc
- use `brew install appledoc` to generate the Third party library doc

###search the library you want in the cocapods library
- use `pod search library_name`
	- like `pod search json`
