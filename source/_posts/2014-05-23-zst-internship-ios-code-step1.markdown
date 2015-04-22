---
layout: post
title: "zst internship IOS code step1"
date: 2014-05-23 11:47:46 +0800
comments: true
categories: IOS Interview
---

###In order to understand better about the code of the project in zst ios project, first list the folder
- in the `huyihui` folder
	- image
	- Third party
	- Sections
	- Controller
	- Model
	- Public
	- AppDelegate.h
	- AppDelegate.m
	- Main.storyboard
	- ViewController.h
	- ViewController.m
	- Images.xcassets
	- Supporting Files
	- Products
- For the project is nearly finished, so I do not introduce the framework they use.
<!--more-->
###First in the `Image` folder
- There are following pics
	- the login picture, the registe picture, the personal center picture, the general picture, the shopping picture, the first page picture, the search picture

###Second in the `Third Party` folder
- mainly used for the ailipay and the shared sdk
- There is a class `AGViewDelegate` which is used for the sharing

###Third in the `Section` folder
- we can see the following
	- ButtonFactory
		- ButtonFactory.h
		- ButtonFactory.m
	- Buttons
		- CreateButton.h
		- CreateButton.m
	- SectionFactory.h
	- SectionFactory.m
	- ButtonMacro.h

- And I think this folder is implement the `factory mode`
- and most of the button is implement in the `CreateButton.m` file

###Fourth in the `Controller` folder
- Here comes `the most important `one
- we can see the following
	- BaseViewController.h
	- BaseViewController.m
	- Mediator
		- CoordinatingController.h
		- CoordinatingController.m
	- login_and_registe
		- {% img /images/internship_zst/1.png %}
	- first_page
		- firstpageandmore(is a tableview that used to show more about the product)
			- {% img /images/internship_zst/2.png %}
		- shopping()
			- {% img /images/internship_zst/3.png %}
			- (those that contrain cell.xib is use to define the layout of the cell of the tableview)
		- detailsoftheproduct()
			- {% img /images/internship_zst/4.png %}
		- tuangou
			- {% img /images/internship_zst/5.png %}
		- preferential_ticket
			- {% img /images/internship_zst/6.png %}
		- HomePageViewController.h
		- HomePageViewController.m
		- HomePageViewController.xib
		- NewProductCollectionView.xib
		- HomeCollectionHeader0.xib
		- HomeCollectionHeader1.xib
		- HomeCollectionHeader2.xib
		- OrdinaryProductImageDetailCell.xib
		- ProductImageDetailCell.xib
		- ProductConstants.h
	- search
		- {% img /images/internship_zst/7.png %}
	- shoppingcart
		- {% img /images/internship_zst/8.png %}
	- comment_and_share
		- {% img /images/internship_zst/9.png %}
	- me
		- AppRecommand
			- {% img /images/internship_zst/10.png %}
		- {% img /images/internship_zst/11.png %}


###Fifth is the `Model`
- we can see the following
- {% img /images/internship_zst/12.png %}

###Sixth is the `Public`
- we can see the following
- {% img /images/internship_zst/13.png %}
- {% img /images/internship_zst/14.png %}
- {% img /images/internship_zst/15.png %}
- {% img /images/internship_zst/16.png %}
- {% img /images/internship_zst/17.png %}
- {% img /images/internship_zst/18.png %}
















