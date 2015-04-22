---
layout: post
title: "how to install python package on redhat without root access"
date: 2014-11-01 00:01:13 -0400
comments: true
categories: python
---
###dependent of scrapy
- remember that the scrapt need python2.7 to run
- and there will be lots of package need to be installed

###What to do when need to install python package on the server without root access
- today I went through a problem that I want to have the python package installed on the high performance server but without the root access
- and what I need to do is to install the python 2.7.3 first and then install all the package that scrapy need and finaly get scrapy run
<!--more-->
###process I use
- And one most important things you need to care about is that 
	- first install python
		- download the python first and compile the package of it.
		- then remember the export the python path to the .bashrc and .bash_profile 
		- so that when you simply type `python` it will not use the default setting of the system
		- or you can type the absolute path of the python and use the python in the bin directory

	- then install the scrapy from source
		- but when you finish install the scrapy
			- you will find out that it will tell you that you do not have some package like Twist , zope, interface and lxml, and cssselect
			- so what you need to do is to fix all this missing stuff 
			- so use `wget` to download the source file of these missing file and install them

		- the will comes the most difficult part
			- when you try to install the lxml
				- you will find out that the system do not have the require of the lxml package
					- the libxml2 and libxslt
					- so what you need to do is to download all the file
					- and build it from source
						- and remember to add prefix and correct all the path error
						- and it would be a good way to output the error log to a file and analyze them using the `>& output file`
						- **and do not hesitate to modify the Makefile or setup.py file when neccessary**
		- also there are problem when try to install cffi and libffi
			- when compile the libffi library
				- remember to include the path of the libffi library when building the cffi
					- use `build_ext -l library_absolute_path -l library2_absolute_path`
	- after install the scrapy successfully
		- use the scrapy executable file in the bin of the scrapy source code
		- `python2.7 ./scrapy crawl linkedin.com`
