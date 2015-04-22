---
layout: post
title: "Linux server tutorial"
date: 2014-04-15 14:47:08 +0800
comments: true
categories: Linux
---

###1.GNU plan
- GNU plan is founded by the Richard M.Stallman and free software foundation
- In order to make sure the GNU software can be used freely
- All the GNU softwares have a license called "GNU General Public License", `GPL`
- this forbid the other from adding any constrict to the GNU software and let all the people to have the right to use it.

###2.POSIX standard
- Portable Operating system Interface for Computing Systems
- used to solve the problem that the UNIX system have lots of versions and result in a chaos
- the standard is developed by the IEEE and standarded by the ANSI and ISO
<!--more-->
###3.Linux component
- Linux kernal
	- is opensource because of the GPL 
- Linux Shell
	- is the UI 
	- have KDE (King Destop Environment) and GROME (GNU Network Object Model Environment)
	- BASH
		- GNU's Bourne Again Shell
- Linux Filesystem
	- multi tree structure

###4.How linux work
####start up
- After the user open the power
	- BIOS first add electivity to check itself and initialize the system and start up the service
	- then start up the mingetty process
- then the shell user log in and start up the device in the sequence setting in the BIOS 
- then start up the GRUB or LILO to get the access of the computer
- after that start up the linux kernel with its configuration
- then use the init program list
- after the user log in successfully, they can enter the system

###5.FTP server
	the ftp is depend on the C/S model
	is used for tranfering the data between client and server
- First the client send the connection request to the server
	- and the client will dynamically open a port > 1024 to wait for the connction of the server
- After the server listened the request in the port 21
	- it will found a ftp connection between client and server
- When need to transfer the data, the client will open a port > 1024 to connect to the pot 20 of the server and transfer the data through the port
- After transferign the data, the port will be released

####ftp software
- we can use `vsFTPd` in linux
- how to setup the ftp server?
	- first `sudo apt-get install vsftpd`
	- and use `sudo /etc/init.d/vsftpd start` to start the service
		- use `sudo /etc/init.d/vsftpd restart` to restart the service
		- use `sudo /etc/init.d/vsftpd stop` to stop the service
	- configure the ftp 
		- use `sudo vi /etc/vsftpd.conf` to edit the configuration file
		- then use `sudo /etc/init.d/vsftpd restart` to restart the service and apply the change
	- also should we backup the file usesudo `cp /etc/vsftpd.conf /etc/vsftpd.conf_back`
	- and do not contain empty line after each sentance

```
	listen=YES             #启用独立vsftpd服务器
	#listen_ipv6=YES       不需要，注释掉
	anonymous_enable=YES   #本服务器需要匿名访问
	local_enable=YES       #要用虚拟用户，需要本地访问的（关于本地用户和虚拟用户不要迷茫，稍后解释）
	write_enable=YES       #需要本地用户对文件进行修改和删除
	#local_umask=022     FTP上传文件权限 ，默认是077，本服务器每个虚拟用户都有上传权限设置，总的就留空注释掉了
	#anon_upload_enable=YES 是否允许匿名用户上传，不需要匿名上传注释掉
	#anon_mkdir_write_enable=YES 是否允许匿名用户的写和创建目录的权限，不要匿名管理，注释掉
	dirmessage_enable=YES 	当切换目录时，是否显示该目录下message隐藏文件的内容，这个用来显示登录信息的 设为YES
	message_file=Welcome     显示的欢迎信息，在ftp目录下建Welcome的文件，里面写上登录信息即可，一般人常用.message隐藏文件
	xferlog_enable=YES 是否激活上传和下载的日志，需要
	connect_from_port_20=YES 是否启动FTP数据端口20的连接请求  需要
	chown_uploads=YES 是否改变上传文件的所有者，我这里需要改变上传文件所有者
	chown_username=virtual 改变上传文件的所有着为virtual，这个virtual用户一会要新建的，用来实现虚拟用户登录
	xferlog日志格式ferlog_file=/var/log/vsftpd.log 上传/下载日志文件所默认的路径
	xferlog_std_format=YES 是否使用标准的ftpd xferlog日志格式
	idle_session_timeout=600 是否将在用户会话空闲10分钟后被中断
	data_connection_timeout=120 是否将在数据连接空闲2分钟后被中断
	#nopriv_user=ftpsecure 是否运行vsftpd需要的非特殊系统用户默认nobody  不需要
	#async_abor_enable=YES 是否是否允许运行特殊的FTP命令async   不要
	ascii_upload_enable=YES 是否启用上传的ascii传输方式   需要
	ascii_download_enable=YES 是否启用下载的ascii传输方式   需要
	ftpd_banner=Welcome to blah FTP service. 用户连接服务器后显示信息，显示信息可以随便写
	#deny_email_enable=YES 是否允许某些匿名用户使用邮件地址（默认的）
	max_clients=10 #FTP服务器最大承载用户,本人设为10
	max_per_ip=5 #限制每个IP的进程
	local_max_rate=256000 #最大传输速率(b/s)
	#hide_ids=YES #是否隐藏文件的所有者和组信息，不隐藏
	idle_session_timeout= 3000  #空闲（发呆）用户会话的超时时间，若是超出这时间没有数据的传送或是指令的输入，则会强迫断线。单位为秒，默认值为300。
```
```
	下面是用来虚拟用户登录的
	^^^^^^^^^^^^^^^^^^^^^^^^^^^^
	guest_enable=YES             使用虚拟用户
	guest_username=virtual       将虚拟用户等同本地用户 virtual
	user_config_dir=/etc/vsftpd/vsftpd_user_conf   虚拟用户配置文件夹
	pam_service_name=vsftpd.vu    虚拟用户加密设置
	^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
```
- 
	- then use `sudo mkdir /home/vsftpd` and `cd /home/vsftpd`
	- then use `sudo mkdir down upload wsn`
	- after that setup the virtual user database
		- use `sudo vi /home/loguser.txt`
		- and the content is 
		```
		down 
		password1
		upload
		password2
		wsn
		password3
		```
	- use `sudo apt-get install db4.7-util`
	- Then create a new dir and put the configuration in it.
	- use `sudo mkdir /etc/vsftpd`
	- use `sudo db4.7_load -T -t hash -f /home/loguser.txt /etc/vsftpd/vsftpd_login.db`
	- set the access of the databases file eventually
	- use `sudo chmod 600 /etc/vsftpd/vsftpd_login.db`
	- configure the PAM file `/etc/pam.d/vsftpd.vu`
	- use `sudo vi /etc/pam.d/vsftpd.vu` with the content
	```
	auth required /lib/security/pam_userdb.so db=/etc/vsftpd_login
	account required /lib/security/pam_userdb.so db=/etc/vsftpd_login
	```
	- PAM is used to verify the virtual user 
		- and this is activated by the command `pam_service_name`
	- Setup the local user for the virtual user
		- setup  a system user called `vsftpd` and the home dir is `/home/vsftpd` and the user login terminal set to /bin/false
		```
		sudo useradd virtual -d /home/vsftpd -s /bin/false
		sudp chown virtual:virtual /home/vsftpd
		```
		- and until now the three users can work now


###6.mail server
	mail is used to communicate on the internet 
- component
	- MUA
		- Mail User Agent
		- used to help the user to send and get the email
	- MTA
		- Mail Transfer Agent
		- used to monitor and send the email
	- mail protocol
		- SMTP
			- simple mail transfer protocol
			- use port 25 
			- is a request/respond protocol
			- and be used to setup the SMTP connection between with the remote server
				- can transfer the mail from client to server 
					- or server to server
		- POP3
			- Post office protocol
			- use TCP 110 port
			- used to receive the mail
			- e.g
				- the client connect with the POP3 server using TCP connection 
				- and the POP3 protocol will affirm the usernamd and userpassword
				- after that the client can receive or delete the mail 
		- IMAP
			- Internet Message Access Protocol
			- can be used as POP3 to receive the mail
			- can be read offline
			- can preview the mail
		- Web Mail
			- is not a protocol but a plugin
			- use the browser to receive, send and read the mail

###7.APT-----software package managemnt 
- use `/etc/apt/sources.list` to store the software package list
	- which is called the *repository*
- this is widely used in the Debain linux like ubuntu
- if the client want to update the software 
	- They will download the dependency file of the softeware and compare with the system file, download all the needed dependencies.
- some useful command
```
apt-get : used to manage the software 
apt-cache : used to check the info of the software
apt-proxy : use to construct the proxy server of APT
apt-show-versions : used to show the version of the software in the system
apt-config : use the read the apt coniguration info 
```

###8.linux user and process management
####user management
- linux have three kinds of users
	- root
	- ordinary
	- virtual
		- like bin, damon, ftp, adm
- each used have a UID(user id)
- `/etc/passwd`
	- used to store the infomation of the users
- `/etc/shadow`
	- used to store the info that passwd file can not store
		- like some info about the password
- and it is similar with the `/etc/group` and `/etc/gshadow`
 

#####use the command to manage

- `whoami`
	- see the name of the current login user
	
- `who`
    - check the current login user
- `w`
	- check the detail info the current login user
- `id`
	- check the UID, GID and so on infomation of particular user 
- `finger`
	- use to see the infomation of particular user
- `su`
	- change the login user
- `write`
	- send message to the particular user
- `wall`
	- broadcast the infomation to all user
- `sudo -s`
	- get the root access
- `useradd` / `adduser`
	- add user
- `passwd`
	- change the password of a user
- `chsh`
	- change the shell the user is using
- `usermod`
	- change the info of the user account
- `userdel`
	- delete the user
- `startx`
	- start the xwindows(GUI)

####process management
#####some useful command
- `ps`
	- see what process is running
	- e.g `ps aux | more`
		- `ps aux | grep httpd`
- `| more`
	- to see the long content in several pages
- `kill`
	- kill the process
	- or `killall`
	- `kill -9 ` to kill the zombie process
	- `pkill name` to kill the process that know its name
- top
	- to see the process dynamically
- `&`
	- let the command work in the background
	- e.g `make install &`
- `Ctrl + Z`
	- put the process in the background and pause it
- `jobs`
	- to see what process is in the background
- `fg`
	- get the background process back
- `bg`
	- run the backgrounf process in the background

###9.linux filesystem
- In the linux filesystem, the file system use inode to store the attibute of the file system.
- if the file pointed by the inode is opened, then the inode += 1
	- else if the file is close, then the inode -= 1
- linux Ext3 filesystem
	- develop the log system depend on the Ext2 system
- linux Swap system
	- used for the exchange area
	- and are used for the memory page to swap the space
	- and not easy to generate the fragment


###10.linux compress
- command
	- `compress`
	- `gzip` and `zcat`
	- `bzip2` and `bzcat` and `bunzip2`
	- `tar`

###11.linux file link
- Symbolic link 
	- soft link
	- use `ln`
	- if the file that is being linked is deleted
		- than the linked file can not be used.

###12.linux disk
- useful command
	- `fdisk`
	- `df`
		- check the information of the disk
	- `fsck`
	- `mount`
		- mount the dir in order to use the disk

###13.linux samba
- a protocol used to communitcate Unix to Windows
- sometimes used to share the file and printer
- SMB protocol is running on the top of the NetBios
- Samba server is made of 
	- NetBios -> NMB
	- SMB

###14.linux NFS server
- NFS is a protocol that used to share the TCP/IP network file with the other.
- This can share the file between different kinds of the operating system
- NFS can make the usage of the disk higher
- And the user do not need to set a home dir one their computer
	- and set the home dir on the remote server
- use dynamic port distribute
	- because the NFS service may use lots of ports
- RPC service mainly used to record the function of the port of the NFS
- and RPC service is used in the port 111
	- when the NFS start, it will select the port that is smaller than 1024

###15.screen 
- split the screen horizontal 
	- `ctrl + a and shift + s`
- split the screen vertical(only in ubuntu/Debian)
	- `ctrl + a and shift + \(|)`
- switch between the screen
	- `ctrl + a + tab`
- after split the screen
	- then create a new windows using
	- `ctrl + a + c`



