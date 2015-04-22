---
layout: post
title: "Introduction to the project of network attack and defense"
date: 2014-04-09 12:20:42 +0800
comments: true
categories: 
keywords: computer secure, c++, peneration testing, hack, winxp, linux, ubuntu, tcp/ip
---


	Produced by pengbin and wangyang
####Abstract
- A kind of penetration testing tool is introduced. And we carry out some experiments to penetrate some systems like WinXP and ubuntu linux. Also will we analyze the mechanic of the penetrating and showing why we can use the vulnerability of the system to get the whole access of it. Thus this kind of testing technology can be used in many areas which can help a good many of companies to protect their personal computer and server from the crackers that want to break into the system and do something bad.
<!--more-->
####What is penetration testing?
- The penetration testing is a kind of technic that can simulate the attacker to attack the target system ,and break their secure system. So that we can finally get the access of it.

- And this kind of test is not completed by a simple steps using a few tools like scanner and so on. Then write a report about it after using them.

- Also, it is impossible to become a good penetration tester in a night.

- And the process of the penetration testing is as follow:
	- Target discovery and enumeration:
		- Identifying the target and collecting basic information about it without making any physical connection with it. 
	- Vulnerability:
		- Implementing various discovery methods such as scanning, remote login, and network services, to figure out different services and softwares running on the target system.
	- Exploitation:
		- Exploiting a known or an unknown vulnerability in any of the softwares or services running on the target system.
	- Level of control after exploitation:
		- This is the level of access that an attacker can get on the target system after a successful exploitation.
	- Reporting:
		- Preparing an advisory about the vulnerability and its possible counter measures. 

####The methodology of the penetration testing
- Here are four famous methodologies in the field of the information security. And this can be used to define the standard steps to take in the penetration testing.

- NIST SP800-115
	- The Technical Guide Information Security Testing is a document carried out by the US government in the field of security testing. 
- ISSAF
	- The Information Systems Security Assessment Framework is an open source testing and analyze framework.
- OSSTMM
	- The Open Source Security Testing Methodology Manual is the international standard of the security testing and analyze, which many enterprise use this as the principal of their daily work.
- PTES
	- This Standard redefines the standard of the penetration testing and make the penetration testing a completely new one. 

####The way of testing
- white box testing
	- One of the advantage is that you know all the knowledge of the system and do not need to worry about being interrupted.

    - But the disadvantage is that you can not test the urgent service of the system.
- black box testing
	- This kind of testing does well in testing the urgent service of the system when being attacked.

    - however, it will need a really good skill to complete the attack.
    
    - Thus, as a black box tester, what you need to do is to find out the cheapest way to get the access of the system.

####Intro of our project
- We are going to build a environment which contains the WinXP , ubuntu linux and Backtrace5 linux operating system connected in innet.

- We will first do the penetration testing on the WinXP and ubuntu platform and provide the way to practice.

- Then We are going to analyze the loopholes and weaknesses of the system and write something to test some loopholes code in order to have a better understanding of the mechanic.

- After introducing the way hackers can use to hack into your computer and we will provide some advises to let you protect your computer better than before.


