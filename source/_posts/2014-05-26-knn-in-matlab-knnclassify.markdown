---
layout: post
title: "KNN in matlab(knnclassify)"
date: 2014-05-26 17:55:05 +0800
comments: true
categories: machine_learning Algorithm
---
- refer from 
	- http://blog.csdn.net/boyxiaolong/article/details/7062394
	- http://blog.csdn.net/aladdina/article/details/4141127

###What is KNN
- simlpy, a method use to classify or regression
- idea
	- 如果一个样本在特征空间中的k个最相 似(即特征空间中最邻近)的样本中的大多数属于某一个类别，则该样本也属于这个类别。
- KNN算法不仅可以用于分类，还可以用于回归。通过找出一个样本的k个最近邻居，将这些邻居的属性的平均值赋给该样本，就可以得到该样本的属性。更有用的方法是将不同距离的邻居对该样本产生的影响给予不同的权值(weight)，如权值与距离成正比。
<!--more-->

###`knnclassify` in matlab
- sample
```
train_data = load('train.csv');
test_data = load('test.csv');

X = train_data(:, 3:3074);
Y = train_data(:, 2);
x = test_data(:, 2:3073);

label = knnclassify(x,X,Y,10,'cosine','random');
```
- knnclassify(test_data,train_data,train_label,numberoflabel,'cosine','random'); 

###main function
- 1.CLASS = KNNCLASSIFY(SAMPLE,TRAINING,GROUP) 
	- 标号和训练数据必须有相同的行数；训练数据和测试数据必须有相同的列；函数对于无效值或者空值会作为丢失值或者忽略这一行。
- 2.CLASS = KNNCLASSIFY(SAMPLE,TRAINING,GROUP,K)
	- 此函数允许你设置距离矩阵形式，如：
		- 'euclidean'    欧氏距离，默认的
        - 'cityblock'    绝对差的和
        - 'cosine'     角度距离
        - 'correlation' 相关距离
        - 'Hamming'      汉明距离
- 3.CLASS =KNNCLASSIFY(SAMPLE,TRAINING,GROUP,K,DISTANCE,RULE)
	- 本函数允许你选择如何对样本进行分类，如你可以选择：
        - 'nearest'  最近的K个的最多数
        - 'random'    随机的最多数
        - 'consensus' 投票法，默认的