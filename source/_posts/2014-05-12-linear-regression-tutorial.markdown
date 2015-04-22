---
layout: post
title: "linear_regression_tutorial"
date: 2014-05-12 15:23:20 +0800
comments: true
categories: Algorithm machine_learning c

---


###First something about training the data
- Training set -> learning algorithm -> hypothesis -> estimated data
- And we will use multiple features.
    - {% img /images/lr_gd/mfeat.png %}

###What is linear regression
- To say the idea in normal, we will have n feature
- And what we are going to do is to observe them and suppose that they should be in a linear method.
- And we should develop a way to find out the parameter to suit the hypothesis function.
<!--more-->
###The first method to solve the problem(Gradient decend)
####how it works?
- There are several ideas
    - **learn rate**
        - if too small, the gradient descent will be slow
        - if too large, the gradient descent will overshoot the minimum.
            - it may be fail to converge, or even diverge
        - {% img /images/lr_gd/apha.png %}
	- **Cost function(J function)**
	    - The cost function has no relationship with the x and y.
	    - and it all depend on the parameter *theta*
	    - and the 1/2 in the front is to make the derivation easier
	    - And the cost function is used to *make the err(the err between hypothesis and real data) smaller*.
	- **Hypothesis**
	    - This function is used to *make the function good*.
	    - good enough to make the y calculate by the function can came close to the real y.
	    - and we will use the err of them to see whether it is good enough or not.
	    - and with all the data, we sum them.
	- **theta**
	    - we can see in the following picture 
	        - suppose that we went down the mountain and we can see all the mountain around us are higher than us
	        - and the theta in the cost function is that we *reduce* theta value in the theta direction 
	        - and the deviation of the cost function on theta i is the distance that we move on theta i direction.
	        
	    - {% img /images/lr_gd/gdpic.png %}
- **Basic algorithm**
    - start with some theta0, theta1, theta2.....
    - Keep changing theta0, theta1, theta2.... to reduce J(theta0, theta2...) until we hopefully end up at a minimum.
    - And this is the key idea of Gradient descend method
- {% img /images/lr_gd/idea.png %}

###The cpp code of it

```
#include<stdlib.h>
#include<stdio.h>
#include<string.h>
#include<math.h>

#define OUTPUTID 10001
#define BUFFERSIZE 50000
#define ROWNUM 10000
#define COLNUM 385

double alpha = 0.1;
char buffer[BUFFERSIZE];
const char *delim = ",";
double x[ROWNUM][COLNUM];
double y[ROWNUM];
double result[ROWNUM];
double diff[ROWNUM];
double theta[COLNUM];
double temp[COLNUM];

void readdata(char *, bool);
void writedata(char *);
void test();
void gradient_descend_train();

int main(){
	readdata("train.csv", true);
	gradient_descend_train();
	readdata("test.csv", false);
	test();
	writedata("predict.csv");
	return 0;
}

void readdata(char *filename, bool haspredicted){
	FILE *inputfile = fopen(filename, "r");

	if(inputfile == NULL){
		system("PAUSE");
		exit(1);
	}
	//drop the first line
	fscanf(inputfile, "%s", buffer);
	//read all lines each
	char *s;
	for(int i = 0; i < ROWNUM; i++){
		
		fscanf(inputfile, "%s", buffer);
		//drop the first column
		strtok(buffer, delim);
		//read the predict y
		if(haspredicted){
			s = strtok(NULL, delim);
			sscanf(s, "%lf", &y[i]);
		}
		//init x0
		x[i][0] = 1;
		//read the matrix
		for(int j = 1; j < COLNUM; j++){
			s = strtok(NULL, delim);
			sscanf(s, "%lf", &x[i][j]);
		}
	}
	fclose(inputfile);
}

void writedata(char *filename){
	FILE *outputfile = fopen(filename, "w");
	
	if(outputfile == NULL){
		system("pause");
		exit(1);
	}

	fprintf(outputfile, "%s,%s\n", "Id", "reference");
	//write the result into file
	for(int i = 0, id = OUTPUTID; i < ROWNUM; i++, id++){
		//cout<<"write the line"<<i + 1<<endl;
		fprintf(outputfile, "%d,%.6lf\n", id, result[i]);
	}
	fclose(outputfile);
}

void initTheta(){  //init theta
	char *thetafilename = "theta.dat";
	FILE *f = fopen(thetafilename, "r");
	for(int j = 0; j < COLNUM; j++)
		fscanf(f, "%lf", &theta[j]);
	fclose(f);
	//init the theta
	for(int j = 0; j < COLNUM; j++)
		theta[j] = 0;
}

void saveTheta(){   //save the theta
	FILE *f = fopen("theta.dat", "w");
	for(int j = 0; j < COLNUM; j++)
		fprintf(f, "%lf\n", theta[j]);
	fclose(f);
}

void calculateResult(){
	for(int i = 0; i < ROWNUM; i++){
		result[i] = 0;
		for(int j = 0; j < COLNUM; j++){
			result[i] += theta[j] * x[i][j];
		}
	}
}

double calculateJ(){
	int turn = 0;
	double cost = 0;
	for(int i = 0; i < ROWNUM; i++){
		diff[i] = result[i] - y[i];
		cost += diff[i]*diff[i];
	}
	cost /= (ROWNUM * 2);
	printf("%5d: J(theta) = %.6lf\n", ++turn, cost);
	return cost;
}

void updateTheta(){
	double sum;
	for(int j = 0 ; j < COLNUM; j++){
		sum = 0;
		for(int i = 0; i < ROWNUM; i++)
			sum += diff[i] * x[i][j];
		theta[j] -= alpha * sum / ROWNUM;
	}
}

void gradient_descend_train(){
	initTheta();
	alpha = 0.1001;
	double cost = 1000;
	while(cost > 26.4){
		calculateResult();
		cost = calculateJ();
		updateTheta();
	}
	saveTheta();
}

void test(){
	calculateResult();
}


```
###The Second method to solve the problem(normal equation)
- This way is a way shown in the statistic learning.
- use the minimum square function to do a regression analyse on the data.
    - {% img /images/lr_gd/nq.png %}
    - and the process is shown : (385*10000)*(10000*385)*(385*10000)*10000*1=385*1
- and we can see the feature normalise in the normal equation function
    - {% img /images/lr_gd/nfn.png %}
    
###The matlab code of it
- The main function

```
%load the train data
data = load('train.txt');
X = data(:, 3:386);
y = data(:, 2);
m = length(y);
m2 = size(X);

%load the test data
data2 = load('test.txt');
feat = data2(:, 2:385);
m3 = size(feat);

sum_test = [0];

%use the equation to calculate
theta = normaleqn(X, y, w);

%calculate the result
result = feat * theta;

csvwrite('aaa_ver3.csv', [linen result]);
```



- The normal equation function

```
function [theta] = normaleqn(x, y, w)
    theta = zeros(size(x, 2), 1);
    %theta = pinv(x' * x + 4000.3 * eye(size(x, 2))) * x' * y;
     %theta = pinv(x' * x + 3.3 * eye(size(x, 2))) * x' * y;
    theta = pinv(x' * x + w * eye(size(x, 2))) * x' * y;
en
```
###The cpp code of it

