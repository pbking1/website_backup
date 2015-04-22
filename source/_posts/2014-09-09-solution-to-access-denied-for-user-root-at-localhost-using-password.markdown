---
layout: post
title: "solution to Access denied for user 'root'@'localhost' (using password:YES) "
date: 2014-09-09 11:49:30 -0400
comments: true
categories: php 
---

###Access denied for user 'root'@'localhost' (using password:YES) 
- in mac
	- open the my.conf in the directory /usr/local/mysql
	- add `skip-grant-tables`
	- restart the mysql service
		- `sudo /usr/local/mysql/bin/mysqld_safe &`
	- then use `mysql -uroot -p` 
		- you can login without password
		- then update the password after `use mysql;`
		- `update user set password=PASSWORD("rootadmin") where user='root';`
	- after that 
		- delete the `skip-grant-tables` add in the my.conf file
	- restart the mysql service
	- then you can use the `mysql -u root -q` to login with your new password
