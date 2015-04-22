---
layout: post
title: "xapian omindex build index and search"
date: 2015-04-15 22:28:58 -0400
comments: true
categories: c++ search_engine
---

###omega is a component that can be used with xapian
- we can use omega to build index

####build index
-  `omindex --db index --url / ./index_file/`
	- --db 后面跟的是索引数据库的名字
	- --url 后面跟的是 / 然后再加上要建索引的数据的文件夹（含有那些要建索引的文件）
- 运行之后，就会生成index文件夹，这个文件夹里面就是建好的索引

####query
- quest --db=index "asd"
	- --db 后面跟的是索引数据库
	- 然后再加上要查询的关键字