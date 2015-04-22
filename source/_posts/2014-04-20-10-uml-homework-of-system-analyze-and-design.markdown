---
layout: post
title: "10 uml homework of system analyze and design"
date: 2014-04-20 12:57:18 +0800
comments: true
categories: UML System_analyze_and_design
---

###1. 概念类图（Conceptual Class Diagram / Domian Model）

- 实验目的：

	- 1. 掌握概念类图的涵义和内容
	- 2. 掌握概念类图的绘制方法
	- 3. 掌握概念类图的使用范围

- 实验内容：

- 1. Read the game description of "Priests and Devils" .
- Priests and Devils
    Priests and Devils is a puzzle game in which you will help the Priests and Devils to cross the river within the time limit. There are 3 priests and 3 devils at one side of the river. They all want to get to the other side of this river, but there is only one boat and this boat can only carry two persons each time. And there must be one person steering the boat from one side to the other side. In the flash game, you can click on them to move them and click the go button to move the boat to the other direction. If the priests are out numbered by the devils on either side of the river, they get killed and the game is over. You can try it in many ways. Keep all priests alive! Good luck!

- and play the game ( http://www.flash-game.net/game/2535/priests-and-devils.html ) first.

- 2. 识别游戏中出现的概念，并画出概念类图。要求给出类、属性、以及类之间的关联（建议有多重性）。
<!--more-->

- 首先概念类图就是领域模型,是对领域内的概念类或者现实世界 对象的可视化表示。并且领域模型并不是对软件对象的描述,他是现 实世界领域中的概念和想象可视化。他不需要方法。
- 其次是设计领域模型的步骤。
- 首先从业务中抽取名词,然后从提取出来的名词中中总结业务实 体,区分名词汇中的属性,角色,实体和实例,形成问题域中的操作 实体的集合。其次是从业务实体集合中抽象业务模型,简历问题域的 概念。最后是用 UML 提供的方法和图例进行领域模型的设计,确定 模型之间的关系。
- 因此我们可以从文本中抽取出包含的类 Priest, Devil, puzzleGame, River, RiverSide, Boat, 另外还有 Player, Clock 类。
{% img /images/hw1.jpg %}

###2. 活动图（Activity Diagram）

- 实验目的：

	- 1.掌握活动图的涵义和内容
	- 2.掌握活动图的绘制方法
	- 3.掌握活动图的使用范围
- 实验内容：

	- 1.选择你熟悉银行的ATM机器，仔细研究观察“人”“机器”对话交互，实现取钱功能的过程。
    - 2.用活动图画出用户取钱的过程。
- 解题思路
	- 1.活动图
		- 活动图是UML用于对系统的动态行为建模的另外一种常用工具，他描述活动的顺序展现从一个活动到另外一个活动的控制流。活动图的本质上是一种流程图。
		- 活动图着重表现从一个活动到另外一个活动的控制流。
		- 也表示一个过程中的多个顺序活动和并行活动。
		- 一旦某个动作完成，紧接着或有一个自动的向外转换。面向对象，着重表现系统的行为而不是处理的顺序。
	- 2.简单的控制流图包含操作，控制流，初始节点，活动最终节点，决策节点，合并节点，注释
	- 3.本体的信息如下
		- 活动主体：用户 ATM机，银行
		- 大致流程：插卡，输入密码，输入取款金额，取款，取卡

{% img /images/hw2.jpg %}

###3. 状态机图（State Machine Diagram）

- 实验目的：
	- 1.掌握状态机图的涵义和内容
	- 2.掌握状态机图的绘制方法
	- 3.掌握状态机图的使用范围
- 实验内容：

- 1.Read the material of "simple digital watch"
	- simple digital watch
    - A simple digital watch has a display and two buttons to set it, the A button and the B button. The watch has two modes of operation, display time and set time. In the display time mode, hours and minutes are displayed, separated by a flashing colon. 
    The set time mode has two sub-modes, set hours and set minutes. The A button is used to select modes. Each time A is pressed, the mode advances in sequence: display, set hours, set minutes, display etc. Within the sub-modes, the B button is used to advance the hours or minutes once each time it is pressed. Buttons must be released before they can generate another event.

- 2.Prepare a state diagram of the watch.

- 3.解题思路
	- 1.状态机图
		- 状态机图显示了对象的生命周期：对象经历的时间，对象的转换和对象在这些时间之间的状态。而且不需要描述所有可能的时间，只需要为具有复杂行为的依赖对象简历状态机图就可以了。
	- 2.状态机图的组件
		- 事件，状态和转换
	- 3.题目解析
		- 题意翻译如下：
			- 有一块电子表，有显示模式，设置时间模式（分为小时和分钟两种子模式），A按钮切换模式，B按钮则是在设置模式下调整时间，按钮不能同时按下去。
- 4.则很容易得出状态机图为
{% img /images/hw3.jpg %}

###4.用例图
- 1.用例图
- 由参与者和用例以及他们之间的关系构成的用于描述系统功能的静态视图称为用例图。
    - 常用于表示系统和环境的上下文
    - 常用于表示参与者和系统交互的目的
    - 对于客户
        - 了解系统满足用户需求提供的服务
    - 开发者
        - 了解系统满足用户需求提供的服务
    - 管理者
        - 早期评估工作的依据
- 2.本题的信息如下
    - 收集整理健康计步软件的资料，主要功能包括卡路里管理，运动规划，运动跑步记录
    - 软件实体
        - 包括人，外部系统，传感器， 时钟
        - 还有利益相关人期望系统达成的目标
- 3.本题的用例图如下
{% img /images/hw4.jpg %}

###5.顺序图
####1.什么是顺序图
    是一种UML行为图。它通过描述对象之间发送消息的时间顺序显示多个对象之间的动态协作。它可以表示用例的行为顺序，当执行一个用例行为时，时序图中的每条消息对应了一个类操作或状态机中引起转换的触发事件。

####2.组成元素
- 角色
    - 系统角色，可以是人或者其他系统，子系统。
- 对象
    - 对象代表时序图中的对象在交互中所扮演的角色，位于时序图顶部和对象代表。
    - 对象一般包含以下三种命名方式：
        - 第一种方式包含对象名和类名。
        - 第二种方式只显示类名不显示对象名，即为一个匿名对象。
        - 第三种方式只显示对象名不显示类名。

- 生命线
    - 生命线代表时序图中的对象在一段时期内的存在。时序图中每个对象和底部中心都有一条垂直的虚线，这就是对象的生命线，对象间 的消息存在于两条虚线间。

- 激活期
    - 激活期代表时序图中的对象执行一项操作的时期，在时序图中每条生命线上的窄的矩形代表活动期。它可以被理解成C语言语义中一对花括号“{}”中的内容。

- 消息
    - 消息是定义交互和协作中交换信息的类，用于对实体间的通信内容建模，信息用于在实体间传递信息。允许实体请求其他的服务，类角色通过发送和接受信息进行通信。

####3.UML三种消息
- 同步消息：发送者等待接收者。
- 异步消息：消息发送后，发送者继续操作，不等待接受者响应，常用于并发。
- 返回消息：表示消息的返回。一般同步（过程调用）的返回不需要画出，直接隐含，而异步返回则可用它。（注：如果异步消息有返回消息，必须明确表示出来）

####4.5-1题目
    小孙从“淘宝网”某商家卖了一部手机，感觉不合适自己决定退货。请仔细研究“淘宝网”的退货业务规程，请将“客户”、“淘宝网”、“商家”三个对象作为主 要参与者，使用系统顺序图描述“淘宝网”退货的业务的系统功能与业务 实现的基本过程。
- 题目解析
    - 系统功能：分发退货的信息。记录退货的信息。退货信息的返还。
    - 业务实现的基本过程：客户向淘宝网发送退货信息、淘宝网将用户的请求提交给商家、商家确认退货信息并将退货消息发给淘宝网、系统修改记录、退货信息返还用户。
    - 1、选择交易，点击退货/退款
    - 2、选择申请服务类型（退货退款/仅退款）
    - 3、选择货物状态和退款原因，填写退款金额和说明，并提交申请
    - 4、等待，卖家同意退货，退货给卖家
    - 5、退货后，请到退款详情页面“填写退货信息”
    - 6、卖家确认收货，退货成功

####5.题目的顺序图
{% img /images/hw5-1.jpg %}


####6.BCE（boundary-control-entity patterns）模式
- 针对每一个用例，可以对应生成一个控制类。
- 参与者对象只能跟边界对象互动。
- 实体对象不能发送消息给边界对象和控制对象。 
- 比较特别的是，如果只是单纯对数据表进行增加、删除、修改、查询的话，可以不设置控制对象，让边界对象直接发送消息给实体对象，以提高整个序列图的执行速度。

####7.业务实体
- 业务实体是业务角色在进行业务活动时使用或产生的事物，在表现形式上可以是一个文档，或者是一个物品的一部分。
- 比如在技术评审管理流程中，评审申请人将提交评审申请材料，专家将对评审材料提出评审意见，因此我们可确定的业务实体是“评审申请”和“评审意见”。每个业务实体通常具有特定的属性，比如“评审申请”业务实体具有的属性包括：申请人、评审类型、评审材料等信息。


####8.题目5.2描述
     在某网上商城系统中，客户可以通过购物车中商品创建订单。请研究从购物车，到提交订单的业务过程，识别以下内容：
     记录过程中使用的页面（UI）
     从页面中识别业务实体（如，用户收件地址，订单）
     假设，系统中有一个订单生成控制器的软件对象，它控制页面流转，处理业务实体信息，保持流程工作状态
     请用顺序图表示 Actor - UIs - Controller - Entities 之间协作完成创建订单任务的过程。

####9.题目的顺序图
{% img /images/hw5-2.jpg %}


- To be continued......