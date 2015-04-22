---
layout: post
title: "php tutorial(1)"
date: 2014-09-08 15:46:01 -0400
comments: true
categories: php
---


###class 1
- how the web site work when you request for the page
    - when you log into the internet, you request for the web server for a file that is the page.
    - if the web server is request for a html file, the server just give it back
    - else if it is the php file, the server send the php file to the php interpreter and process the php
        - and after the process, the interpreter give it back 
        - (for php is an interpret kind of language and it do not need to be compile)
        - and then the server send the php file back to the web browser
    - if the php is interacting with the database, then the code of the php will have sql query with the database.
        - after the query, send back to the php interpreter and then send back to the server and then send back to the web browser
<!--more-->  

- All in all, there are can be three layer in the environment
    - the front is the browser
        - html, css, coding logic
    - the middle is the server 
        - web server and php interpreter
    - the database aspect is the third
        - mysql database engine
        - phpMyAdmin(DBMS)
- the php interpretation run from the top of the file to the bottom of the top

###class 2
- '' these two symbol can be the end of the string
- the HEREdoc mechnic is the 
    - remember that the final HERE should have no space in front of it
```
print <<<HERE
        <p></p>
HERE;
```
- or you can use the filter_input method to validate the email easily.
    - such as without "." "space" and so on.