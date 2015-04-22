---
layout: post
title: "use sqlite in html5"
date: 2014-06-09 10:50:05 +0800
comments: true
categories: html Android
---

- There are three ways to store data using html5
	- using database (sqlite)
	- using localStorage
		- will only store on client, will not send to server
		- this data can be read even using different block on the same browser
		- the data will not disapear unless you delete it
	- using sessionStorage
<!--more-->
- The localStorage and sessionStorage are storing the data on your computer and after the web page is loaded
	- we can use javascript to get the data


- running the first time
	- use all the following code can see the db insert and query successfully
- but in the second time
	- you should note the create and insert
	- then you can see the result

```
<html>
	<body>
		<script type="text/javascript">
			//the first way to store the data
			if(localStorage.pagecount){
				localStorage.pagecount = Number(localStorage.pagecount) + 1;
				}else{
				localStorage.pagecount = 1;
			}
			document.write("Visits: " + localStorage.pagecount + " time(s).");

			//the second way to store the data
			//using sqlite
			var db = openDatabase("mytestdb", "1.0", "stu list", 1024*1024, function(){});
			//use the command `openDatabase` can create a data base
			//name, version, discription, db size
			alert("<p>create db success</p>");
			db.transaction(function(tx){
					tx.executeSql("CREATE TABLE IF NOT EXISTS test(id int UNIQUE, title TEXT, content TEXT)");
					document.write("<p>create table test successfully</p>");
					tx.executeSql("insert into test(id, title, content) values(1, '111', 'swq')");
					tx.executeSql("insert into test(id, title, content) values(2, 'bbb', 'sawf')");
					document.write("<p>insert two contents successfully</p>");
					tx.executeSql("SELECT * FROM test", [], function(tx, rs){
						var len = rs.rows.length;
						alert(len + "");
						for(var i = 0; i < rs.rows.length; i++){
							var testObj = rs.rows.item(i);
							alert(testObj.id + "-----" + testObj.title);
						}
					});
			});
		</script>
	</body>
</html>

```