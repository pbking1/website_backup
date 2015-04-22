---
layout: post
title: "iupui mason high performance mass"
date: 2014-11-05 20:55:25 -0500
comments: true
categories: other high_performance
---

###In the iupui mason server
- there are 20 server, each have 10 gigabit ethernet 
- 4 cpu in each server
	- 8 core processor each cpu
	- total 32 core in each server
- in the /scratch or /tmp there are total 400 GB disk storage
	- and the file will be delete after 14 days since they are created
	- 
<!--more-->
###when login
- use "username@mason.indiana.edu"
	- will result in two server
		- h1.mason.indiana.edu
		- h2.mason.indiana.edu

###cpu/memory limit
- user process on login node are limited to 20 minutes CPU time
	- if exceeded, will be killed automatically
- use TORQUE `qsub` to submit job that need more than 20 minutes cpu time
	- `qsub`
		- `qsub -l walltime=10:00:00 job.script`
			- for the system default time is 60 minutes
				- so use walltime to use more time
		- `qsub -l nodes=1:ppn=2 job.script`
			- run the script in a node and using two core processers
		- `qsub -l nodes=4:ppn=31,vmem=100gb -l walltime=20:00:00 jobscript.script `
			- if use multi commands, use `-l` to separate the argument 

	- `qstat`
		- `qstat -a`
			- display all job
		- `qstat -n`
			- list the nodes allocated to a job
		- `qstat -r`
			- list the job that are running
		- `qstat -u username@host`
			- display the job owned by the username
	- `qdel`