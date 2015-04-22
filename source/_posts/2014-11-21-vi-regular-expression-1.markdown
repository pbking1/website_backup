---
layout: post
title: "vi regular expression and data processing(1)"
date: 2014-11-21 15:07:04 -0500
comments: true
categories: Linux vim
---

###data processing is very important before data mining
- like if you are going to do some data mining in the linkedin public profile
- 1.find out the number of the people that have
       - education
       - experience
       - skills
       - have all
- 2.find out all the skills and list the number of user who own them in a diagram
- 3.find out all the company number
- 4.find out all the people that is in US
- 5.find out all the education level of all people
       - like undergraduate, graduate, phd
- 6.find out all the experience about job numbers
       - like 1 job, 2 jobs, 3 jobs
<!--more-->

###regular expression in VIM
- delete the line that match the particular format
	- like match all the lines in a document that match 'name: current'
		- :%s/^name:\tcurrent.*$//g
		- :%s/skill_num:0\n//g

###count the number
- the number of the education, the number of the experience and the number of the skill
	- like
		- grep 'skill_num' *.txt > ./checklist/skill_num.txt
			- :%s/output[1-9][0-9]*.txt:skill_num://
				- delete the tag
		- grep 'experience_num' *.txt > checklist/exp_num.txt
			- :%s/output[1-9][0-9]*.txt:experience_number://
				- delete the tag
		- grep 'education_nun' *.txt > ./checklist/edu_num.txt
			- :%s/output[1-9][0-9]*.txt:education_nun://
				- delete the tag before the number

- use the number of the education, experience and skills to plot the tendency
```
clear all;
clc;
edu = csvread('edu.csv');
exp = csvread('exp.csv');
skill = csvread('skill.csv');

figure

%education number
edu_res = zeros(size(edu));
edu = sort(edu);
for i=1:size(edu)-1
   if edu(i) == edu(i + 1)
       edu_res(edu(i)) = edu_res(edu(i)) + 1;
   elseif edu(i) ~= edu(i + 1)
       edu_res(edu(i+1)) = edu_res(edu(i+1)) + 1;
   end
end

subplot(3,1,1); %add plot into one image
plot(edu_res(1:15, :));
title('education line plot')
xlabel('index of education number')
ylabel('number of the people')

%experience number
exp_res = zeros(size(exp));
exp = sort(exp);
for i=1:size(exp)-1
   if exp(i) == exp(i + 1)
       exp_res(exp(i)) = exp_res(exp(i)) + 1;
   elseif exp(i) ~= exp(i + 1)
       exp_res(exp(i+1)) = exp_res(exp(i+1)) + 1;
   end
end

subplot(3,1,2); %add plot into one image
plot(exp_res(1:43, :));
title('experience line plot')
xlabel('index of experience number')
ylabel('number of the people')

%skill number
skill_res = zeros(size(skill));
skill = sort(skill);
for i=1:size(skill)-1
   if skill(i) == skill(i + 1)
       skill_res(skill(i)) = skill_res(skill(i)) + 1;
   elseif skill(i) ~= skill(i + 1)
       skill_res(skill(i+1)) = skill_res(skill(i+1)) + 1;
   end
end

subplot(3,1,3); %add plot into one image
plot(skill_res(1:50, :));
title('skill line plot')
xlabel('index of skill number')
ylabel('number of the people')
```

###diff the file
- diff whole_file subfile | grep "< " | sed 's/< //g'
  - using this command can get all the content in the subfile out of the wholefile

###if you want to separate one very long string 
- use "\r" to replace "," not "\n" in vim
- or use 
  - `tr ", " "\n"`

###erase the empty line
- `sed 's/^*$//g' file`

###replace the ^M into \n
- use 's/\r/\r/'

###in vim use \r as "enter button"

###sort the file use the sequence of first line
- `sort -n -k1,1` filename