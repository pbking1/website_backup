---
layout: post
title: "database_and_backend_injection"
date: 2014-10-23 09:13:16 -0400
comments: true
categories: database php
---

###database ER diagram
- {% img /images/php_project/lab4_db.jpg %}
- some change in the database **relationship**
- <img src="/images/php_project/database_lingma_structure.png" style="height: 300px; width: 300px">
- we have 
	- T_ADMIN
	- T_USER
	- T_USER_CLASS
	- T_PROJECT
	- T_PRO_LEVEL
	- T_PROJECT_STATISTICS
	- T_TASK
	- T_SUBTASK
	- T_MATERIAL
	- T_CUSTOMER

<!--more-->
- **Table structure** 
- {% img /images/php_project/1.png %}
- {% img /images/php_project/2.png %}
- {% img /images/php_project/3.png %}
- {% img /images/php_project/4.png %}
- {% img /images/php_project/5.png %}
- {% img /images/php_project/6.png %}
- {% img /images/php_project/7.png %}
- {% img /images/php_project/8.png %}
- {% img /images/php_project/9.png %}
- {% img /images/php_project/10.png %}
###database insertion
- database connection
```
$conn = mysql_connect("localhost","pengbin","pengbin");
mysql_select_db("pengbin_db", $conn);
```

- database insertion
```
$sql = "insert into T_CUSTOMER (CustomerName, CustomerAddress, Notes, Active) values ('$_POST[name]','$_POST[address]','$_POST[note]','$_POST[Active]')";
mysql_query($sql, $conn);
```