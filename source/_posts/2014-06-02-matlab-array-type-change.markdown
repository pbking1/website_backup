---
layout: post
title: "matlab array type change"
date: 2014-06-02 14:57:28 +0800
comments: true
categories: matlab
---

###How to convert between cell, double and char array?
- there are three type of array in matlab
	- cell array
	- double array
	- char array
<!--more-->
####How to convert double array to char array?
- use `num2str` or `mat2str`

####How to convert char array to double array?
- use `str2num`<0.0001> and `str2double`<0.01> 

####How to convert cell array to char array?
- use `cell2mat`

####How to convert char array to cell array?
- use `cellstr`

###How to convert cell array to double array?
- use `cell2mat` and `str2num`

####How to convert double array to cell array?
- use `num2cell`