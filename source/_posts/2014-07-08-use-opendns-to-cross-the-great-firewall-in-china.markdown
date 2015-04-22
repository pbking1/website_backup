---
layout: post
title: "use opendns to cross the great firewall in China"
date: 2014-07-08 15:22:39 +0800
comments: true
categories: other

---

###once upon a time
- we can log in facebook and google directly
- but nowadays we can not
- and because DNS hijacking and DNS cache posioning, we can not log in directly anymore
<!--more-->
###what is DNS hikacking?
- DNS hijacking(劫持)
- to simplifiy the idea
	- when you type in google.com, you will not attach the google.com
		- you will be direct to the baidu.com
	- and this is the DNS hijacking
- **and the reason why this will happen is that the DNS server is cracked and the domain name will be parse to the wrong ip.**
- and recently the govenment is using this kind of strategy

###what is DNS cache posioning?
- DNS污染
- this idea used to be used to block the youtube, facebook website
- this is on the protocol layer
- and the mechisim is that when you want to launch the particular website
	- the port 53 UDP is check and when they found that you want to attach particular website, they will change the domain name parse DNS server into a wrong one and then you will not be able to get the correct ip.
	- then you will not be able to get to the website.

###How dns works?
- first, when we use some domain name like "www.facebook.com"
	- and when we type the domain name into the website
		- the website will send the name to the dns server to check the ip
		- then return the ip the our computer
		- then we will know the ip of the target website 
			- and we will be able to get to the website

###why can we use this in China?
- Because in China when you type "www.google.com"
- they block the dns parse not the connection
	- so we will be able to break through the wall if we use the other dns server to help use parse the domain name

###how to use opendns
- change the dns settings in the PC or laptop
	- if you want to use the google dns 
		- set "8.8.8.8" and "8.8.4.4"
	- if you want to use the opendns
		- set "208.67.222.222" and "208.67.220.220"
		- or set "42.120.21.30" and "221.10.251.52"
- then if you are using Max 10.8 or above
	- you can renew the dns setting using 
		- "sudo killall -HUP mDNSResponder"

###when not to use opendns
- when you are using the payment or something private
	- do not use opendns
