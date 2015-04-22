---
layout: post
title: "matlab classification method"
date: 2014-06-02 15:15:11 +0800
comments: true
categories: matlab machine_learning
---

###The method in the system
- MultiNomial logistic Regressoin
	- bad in high dimension
		- `Factor = mnrfit(train_data, train_label);`
		- `scores = mnrval(Factor, test_data);`
<!--more-->
- Random Forest
	- good classifier
	- score is the probability output
		- `Factor = TreeBagger(numberoftree, train_data, train_label);`
		- `[predict_label, scores] = predict(Factor, test_data);`
	
- Navie Bayes
	- `Factor = NaiveBayes(train_data, train_label);`
	- `Scores = posterior(Factor, test_data);`
	- `[Scores, predict_label] = posterior(Factor, test_data);`
	- `predict_label = predict(Factor, test_data);`
	- `accuracy = length(find(predict_label == test_label))/length(test_label)*100;`
- SVM
	- `Factor = svmtrain(train_label, train_data, '-b 1');`
	- `[predict_label, accuracy, scores] = svmpredict(test_label, test_data, Factor, '-b 1');`
- KNN
	- `predict_label = knnclassify(test_data, train_data, train_label, num_neighbors);`
	- In matlab 2012
		- `Factor = ClassificationKNN.fit(train_data, train_label, 'NumNeighbors', numofneighbours);`
		- `[predict_label, scores] = predict(Factor, test_data);`
- Ensembles for boosting, Bagging or Random Subspace
	- In matlab2012
		- `Factor = fitensemble(train_data, train_label, 'AdaBoostM2', 100, 'tree');`
		- `Factor = fitensemble(train_data, train_label, 'AdaBoostM2', 100, 'tree', 'type', 'classification');`
		- `Factor = fitensemble(train_data, train_label, 'SubSpace', 50, 'KNN');`
		- `[predict_label, scores] = predict(Factor, test_data);`
- discriminant analysis classifier
	- `Factor = ClassificationDiscriminant(train_data, train_label);`
	- `Factor = ClassificationDiscriminant(train_data, train_label, 'discrimType', 'non-linear...');`
	- `[predict_label, scores] = predict(Factor, test_data);`