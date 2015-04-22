---
layout: post
title: "virtual machine windows VS2010 UNC path not support"
date: 2015-04-14 21:17:08 -0400
comments: true
categories: windows vs
---

###解决UNC路径不受支持
	在虚拟机的VS2010中编译出错

- 错误提示：用作为当前目录的以上路径启动了 CMD.EXE。 UNC 路径不受支持。默认值设为 Windows 目录。系统找不到指定的文件。执行 c:\windows\system32\cmd.exe 时出错.
- 解决方法:
	- 在注册表中,添加一个值即可.路径如下:
   		- HKEY_CURRENT_USER\Software\Microsoft\Command Processor               
		- 添加值 DisableUNCCheck，类型为 REG_DWORD 并将该值设置为1 （十六进制）。
	- 或者，打开cmd.exe
		- 把下面这行代码复制进去，按回车
		- reg add  "HKEY_CURRENT_USER\Software\Microsoft\Command Processor" /v DisableUNCCheck /t REG_DWORD /d 1 /f