---
layout: post
title: "C pointer tutorial (1)"
date: 2014-04-25 13:41:01 +0800
comments: true
categories: c
---

###First is the basic
- About `#`
	- these code are processed by the preprocessor
	- After the preprocessor read the code, the preprocessor directives will deal with it
	- then give the main code that are dealed with by the preprocessor directives to the complier
	- like `#include <stdio.h>`
		- It means that use the content in the stdio.h to replace the `#`
- About `const`
	- the value that is named const can not be modified
	- and it would be better to use `const` than `define` to define some const value.
- About passing the value
	- in C programming language
		- all the array is passed using **reference**(if the value change in the function, it will change.)
		- and all the value and const value are passed using **value**(if the value change in the function, it will **not** change.)

- About string I/O
	- `gets`
		- it is used to read a line in the content and store it as a parameter to pass to the array
		- the input line contains: a string and a newline
	- `puts`
<!--more-->
- About `*`
	- **the pointer point the address of a value that is stored in the memory**

###data type
- In C programming language, there are only 4 basic data type
	- int, float, pointer and polymerization
- **INT**
	- contains : char, short, int and long int
	- signed and ubsigned
	- thr range of the variable

	type|range
	----|------
	char|0~127
	signed char|-127~127
	unsigned char| 0~255
	short int|-32767~32767
	unsigned short int|0~65535
	int|-32767~32767
	unsigned int|0~65535
	long int |-2147483647~2147483647
	unsigned long int | 0~4294967295

	- short int is at least 16 bits
	- long int is at least 32 bits
	- if the computer is 32 bits then int is 32 bits
		- else if the computer is 64 bits than the int is 32 bits
	- The range difference in difference kinds of machine

	data type|32 bits compiler|64 bits compiler
	-----|-------|--------
	char|1 byte | 1 byte
	char *|4 bytes| 8bytes
	short int|2 bytes|2 bytes
	int|4 bytes|4 bytes
	unsigned int|4 bytes | 4 bytes
	float | 4 bytes | 4 bytes
	double | 8 bytes | 8 bytes
	long | 4 bytes | 4 bytes
	long long | 8 bytes | 8 bytes
	unsigned long | 4 bytes | 8 bytes 

	- use `sizeof(data type)` to get the length of the data type
	- add `0` before number to make it octal number
	- add `0x` before number to make it hexadecimal number
	- add `L` before character to make it wider charactor literal(it the environment support)
		- e.g `L'X'`
- **FLOAT**
	- contains : float, double, long double
	- range : 10^-37 ~ 10^37
	- in 
