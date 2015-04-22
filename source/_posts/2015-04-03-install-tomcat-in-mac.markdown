---
layout: post
title: "install tomcat in mac"
date: 2015-04-03 03:28:36 -0400
comments: true
categories: java
---

###install tomcat in mac
- 1.go to http://tomcat.apache.org/ and download the zip file of tomcat
- 2.then unzip the zip file into /Library and rename into "Tomcat"
- 3.then `sudo chmod 755 /Library/Tomcat/bin/*.sh `
- 4.if you want to start tomcat
	- `sudo sh startup.sh` 
	- if want to stop
		- `sudo sh /Library/Tomcat/bin/shutdown.sh`