---
layout: post
title: "ASP.net in mac MonoDevelop"
date: 2015-04-14 03:01:35 -0400
comments: true
categories: c# asp.net
---

###install asp.net environment in mac
- we can use MonoDevelop IDE in mac to develop c# or VB program
	- also asp.net too
- download url: http://www.monodevelop.com/download/
	- download the Xamarin studio as development IDE
<!--more-->
###after install the environment
- start a solution as ASP.NET project in C#
- it will generate a project with some default page
	- The Default.aspx can be act as a html page
	- and Default.aspx.cs can act be a controller in c#
	- and Default.aspx.designer.cs can act be a model in MVC

###connect to mysql
- remember to add System.Data in the Reference
- add a MyDql.Data in Packages
- add a `using MySql.Data.MySqlClient; ` in the cs code

###code for mysql connection
- front end page

```
	<%@ Page Language="C#" Inherits="test1.Default" %>
	<!DOCTYPE html>
	<html>
	<head runat="server">
		<title>Default</title>
		<style>
		table, th, td {
		    border: 1px solid black;
		    border-collapse: collapse;
		}
		th, td {
		    padding: 15px;
		}
		</style>
	</head>
	<body>
		<form id="form1" runat="server">
			<asp:button id="clickMeButton" runat="server" text="Click Me" onClick="clickMeButton_Click" />
			<asp:label id="outputlabel" runat="server" />
		</form>
	</body>
	</html>
```
	


- backend
- cs file 1
```
	<code>
	using System; 
	using System.Data; 
	using System.Configuration; 
	using System.Collections; 
	using System.Web; 
	using System.Web.Security; 
	using System.Web.UI; 
	using System.Web.UI.WebControls; 
	using System.Web.UI.WebControls.WebParts; 
	using System.Web.UI.HtmlControls; 
	using MySql.Data.MySqlClient; 
	namespace test1
	{
		public partial class Default : System.Web.UI.Page
		{
			public void clickMeButton_Click (object sender, EventArgs e)
			{
				object val = ViewState["ButtonClickCount"];
				int i = (val == null)? 1 : (int)val + 1;
				outputlabel.Text = string.Format ("You clicked me {0} {1}", i, i==1?"time":"times");
				ViewState["ButtonClickCount"] = i;
				string query = "select * from reference limit 10"; 
				MySqlConnection myConnection = new MySqlConnection("server=localhost;user id=root;password=root;database=reference_db"); 
				MySqlCommand myCommand=new MySqlCommand(query,myConnection); 
				myConnection.Open(); 
				myCommand.ExecuteNonQuery(); 
				MySqlDataReader myDataReader = myCommand.ExecuteReader(); 
				string bookres=""; 
				bookres += "<table style=\"width:100%\">";
				while (myDataReader.Read()==true) 
				{ 
					bookres += "<tr><td>";
					bookres+=myDataReader["id"]; 
					bookres += "</td><td>";
					bookres+=myDataReader["ReferenceType"]; 
					bookres += "</td><td>";
					bookres+=myDataReader["Record_Number"]; 
					bookres += "</td></tr>";
				} 
				bookres += "</table>";
				myDataReader.Close(); 
				myConnection.Close(); 
				outputlabel.Text = bookres;
			}
		}
	}
```

- cs file 2
```
	<code>
	using System;
	using System.Web;
	using System.Web.UI;
	namespace test1
	{
		public partial class Default
		{
			protected System.Web.UI.WebControls.Button button1;
			protected System.Web.UI.WebControls.Label outputlabel;
		}
	}
    </code>
```
