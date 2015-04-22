---
layout: post
title: "Basic idea of MVC"
date: 2014-05-03 21:21:20 +0800
comments: true
categories: System_analyze_and_design
---

###What is MVC?
- MVC模式（Model-View-Controller）是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：模型（Model）、视图（View）和控制器（Controller）。
- MVC在这几年应该被非常多的人所熟悉了，因为相当多的web框架采用的是这套架构，此外，早在MFC横行的年代，MFC所采用的document/view架构也是MVC架构的变种。包括QT，它的model/view亦是如此。只不过它们都将MVC中的view和controller的功能整合到了一起。
- MVC的全称是model-view-controller architecture，最早被用在了smalltalk语言中。MVC最适合用在交互式的应用程序中。
<!--more-->
###The component of it
- View
	- V：View，就是所谓的视图，是用户看到并与之交互的界面。对老式的Web应用程序来说，视图就是由HTML元素组成的界面，在新式的Web应用程序中，HTML依旧在视图中扮演着重要的角色，但一些新的技术已层出不穷，它们包括Macromedia Flash和象XHTML，XML/XSL，WML等一些标识语言和Web services.
- Model
	- M：Model，就是所谓的模型，表示企业数据和业务规则。在MVC的三个部件中，模型拥有最多的处理任务。例如它可能用来处理数据库。被模型返回的数据是中立的，就是说模型与数据格式无关，这样一个模型能为多个视图提供数据。由于应用于模型的代码只需写一次就可以被多个视图重用，所以减少了代码的重复性。
- Controller
	- C：Controller，就是所谓的控制管理器，是用来同步M与V的。控制器接受用户的输入并调用模型和视图去完成用户的需求。所以当单击Web页面中的超链接和发送HTML表单时，控制器本身不输出任何东西和做任何处理。它只是接收请求并决定调用哪个模型构件去处理请求，然后用确定用哪个视图来显示模型处理返回的数据。

###MVC architecture
- 从下图中，可以看出控制器就是一个中枢，MVC的处理过程就是在用户产生行为，提交表单的时候，由Controller来制定哪一个Model来对用户行为进行处理，并且在处理后将结果返回给View，用以给用户进行显示。
- {% img /images/system_anaylze_mvc1.png %}

###Something important about MVC
- 1.MVC将数据的维护和数据的呈现，与用户的交互割裂了。Model负责的是数据的维护，就好比是DB和文件要保存数据一样，可以认为它是process。而view负责的是数据的呈现，把数据通过某种形式在用户面前展现，把它看做是output。
	- 而controller负责的是处理用户的输入。它提供一个窗口或者是控件供用户输入数据，它就是input。所以，一个MVC架构，就是将交互式程序的process，input和output解耦合。
- 2.第二点更为重要，就是model与view和controller之间的联系。任何一个MVC框架都必须提供一个“change-propagation mechenism”(变更-传播机制)。而这个变更-传播机制是MVC框架中model和view以及controller之间的唯一的联系（The  change-propagation mechanism  is  the  only  link  between  the model and the views and controllers）。
	- 比如说，一个用户通过controller改变了model中的数据，那么model会使用变更-传播机制来通知和它有关的view和controller，使得view去刷新数据和重新显示。
	- 有很多人总是对于MVC架构不能够熟练掌握，核心问题就在于他在使用MVC架构的时候是看不到变更-传播系统的，所以对于MVC架构的内在运行机制无法了解。

###The process of MVC
- {% img /images/system_anaylze_mvc2.png %}
- 1.用户操作controller，相当于调用controller的handleEvent函数；
- 2.handleEvent函数实际上调用的是model中的成员函数，对model中的数据进行操作；
- 3.model中的数据被调用完成后，model会执行自身的notify函数；
- 4.notify函数会调用和这个model有关的所有view和controller的update函数；
- 5.update函数会调用各自的display函数和getData函数；
- 6.当这一切都完成时，handleEvent才返回；



###MVC usage
- Android中界面部分也采用了当前比较流行的MVC框架，在Android中：

	- 视图（View）
		- 一般采用XML文件进行界面的描述，使用的时候可以非常方便的引入。当然，如何你对Android了解的比较的多了话，就一定可以想到在Android中也可以使用JavaScript+HTML等的方式作为View层，当然这里需要进行Java和JavaScript之间的通信，幸运的是，Android提供了它们之间非常方便的通信实现。
	- 控制器（Controller）
		- Android的控制层的重任通常落在了众多的Acitvity的肩上，这句话也就暗含了不要在Acitivity中写代码，要通过Activity交割Model业务逻辑层处理，这样做的另外一个原因是Android中的Acitivity的响应时间是5s，如果耗时的操作放在这里，程序就很容易被回收掉。
	- 模型（Model）
		- 对数据库的操作、对网络等的操作都应该在Model里面处理，当然对业务计算等操作也是必须放在的该层的。就是应用程序中二进制的数据。

