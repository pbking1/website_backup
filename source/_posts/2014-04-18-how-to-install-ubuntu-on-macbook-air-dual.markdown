---
layout: post
title: "How to install ubuntu on macbook air dual"
date: 2014-04-18 11:07:34 +0800
comments: true
categories: Linux
---

####1.For there are too many software that can be used in ubuntu not in OSX so I decided to install ubuntu on my macbook air
- I have try the mac version ubuntu and *it do not work*
- and the origin version for windows is work on mac

####2.First use `Unetbootin` to create a usb bootable ubnutu on mac
- There are two ways to finish this
- The first is(I do not succeed in this)
	- `diskutil list`
		- show the disk that is mounted on your mac
	- then insert the usb
	- run `diskutil list again`
		- and determine the device node assigned to the usb like `disks1s2`
	- then `diskutil unmountDisk /disks1s2`
	- after that `sudo dd if=/path/to/ubuntu.img.dmg of=/dev/disks1s2 bs=2m`
		- to create the bootable usb ubuntu
		- and the bs is the I/O speed and the max is 2m
	- It may cost some time to complete
	- finally run `eject /dev/disks1s2`
- The second is
	- use the `Unetbootin` to create the bootable usb directly
<!--more-->

####3.Then we need the split the disk
- search `Disk Utility`
- open it and get to the `partition`
- click '+' to create a partition of 40 GB
	- partition it in the MS-DOS(FAT)
- and click '+' again to create a patition of 2 GB
	- make the swap sizeMS-DOS(FAT)
	- name the partition "swap"
	- restart the computer and press alt/option key when starting

####install ubuntu
- when being asked for `installation type`
	- choose something else to partition by ourselves
	- select `ext4` and mount `/` in the 40GB disk
	- select `swap area` for the swap disk
- and nothing else should be difficult

####after installing ubuntu successfully on mac you should do
- `sudo apt-get install macfanctld` to enable the fan and sensor
- `sudo apt-get install update && sudo apt-get upgrade` to update the system and get wifi work(you may not get wifi work at the first time you start the system, so get a wired network and upgrade the system)
- `sudo apt-get install flashplugin-installer` to install the adobe player
- `sudo add-apt-repository ppa:linrunner/tlp`
	- `sudo apt-get update`
	- `sudo apt-get install tlp tlp-rdw`
	- `sudo tlp start` 
	- to improve battery life and reduce overhearting

####some configuration of ubuntu
- first is the system mointer
	- `conky`
	- install conky manager and you can get lots of theme of it
	- and I have to say thats really cool
	- `sudo apt-add-repository -y ppa:teejee2008/ppa`
	- `sudo apt-get update`
	- `sudo apt-get install conky-manager`
- second is the byobu terminal
	- `sudo apt-get install byobu`
	- and set the start up script in the `/use/bin/byobu`
	- and the terminal will start up in byobu
	- `fn + F2` to  create a new terminal
	- `fn + F3` and `fn + F4` to switch the terminal
- and `tilda`, `guake` will be good choice of terminal
	- press `F12` can drop down the guake terminal

####if there is error
- if face `xinit: server error`
	- run `sudo apt-get install --reinstall xorg`
	- and it may help

