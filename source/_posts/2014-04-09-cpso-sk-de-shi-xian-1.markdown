---
layout: post
title: "CPSO-Sk 的实现(1)"
date: 2014-04-09 00:36:53 +0800
comments: true
categories: Algorithm
keywords: algorithm, cplusplus, c, pso
---

- 其实和标准的PSO是一样的
- 只是初始种群是不一样的
    - 假设标准版的种群大小是100的话，那么
    - 这个版本是把100分成10份，然后再对每一份使用标准版的算法
    
- 因此这两个算法本质上没有区别，只是初始种群大小不一样而已
<!--more-->
- 以下是伪代码

###伪代码
- 假设我们的算法初始种群分成10份

```
如何初始化：
for i=0:种群大小
    for j=0:维度{
        对每个个体的位置进行随机化
        对每个个体的速度进行随机化
        对每个个体的最佳位置为粒子的位置
    }
for i=0:种群大小{
    计算适应度
    把每个粒子的最佳适应度初始化为初始值
}
把全局最优初始化为0     
```

```
更新局部最优值
if(如果粒子的最佳适应度比现在的适应度 大)
    for i=0:维度
        把粒子的历史最佳更新为粒子的位置
    把粒子的最佳适应度更新为粒子现在的适应度
```

```
全局最优：
if(索引为0)
    for i=1:种群大小
        if(适应度小于索引第一个粒子的适应度){
            把s=第i个粒子的适应度
            flag=i
        }
    for i=0:维度
        把全局最优位置更新为第flag个的位置
    把全局最适应的值更新为第flag个的适应值
else{
    for i=0:种群大小
        if（如果最佳适应值小于全局最优）{
            for i=0:维度
                把最佳适应度更新成现在这个粒子的最佳适应度
            把全局最佳适应度更新为现在粒子的最佳适应度
        }
}
```

```
计算适应值函数
```


```
首先把种群分成10份，为了方便起见，相当于每相隔10个就停止然后对这10个粒子用PSO
然后就开始对包含10个粒子的子种群
    定义最大循环次数，建立一个循环
        if（达到最大循环次数或者满足停止条件）
            输出最佳适应值和取得这个值所需要的迭代次数
        else{
            for i=1:种群大小{
                for i=1:维度{
                    更新个体速度：使用公式一
                    判断速度是否超过最大速度
                        如果超过了就把速度更新给最大速度
                    判断位置是否越界（小于最小值或者大于最大值）
                        乘上对应边界的两倍再减掉现在的位置
                }
                计算适应值
                计算局部最优解
            }
            计算全局最优
        }
```
###C++ source code
```
#include<iostream>
#include<cmath>
#include<cstdlib>
#include<cstdio>
#include "data.h"

using namespace std;
#define C1 2
#define C2 2
#define VMAX 5.0
#define Iteration 10000
#define rand1() (double)(rand() / (double)RAND_MAX)
double global_best = 10000.0;
double v[100000] = {0};
const int X_const = 5;
double time_pso = 0.0;


struct particle{
	double current;
	double personal_best;
};

struct particle p[100000];

double fitness(double x){
	return x * x - 20 * x + 100;
}

void init(){                                                                                                                                
	int i;                                                                                                                                     
	for(i = 0; i < 100000; i++){                                                                                                            
		p[i].current = -2 + i;                                                                                                                 
		p[i].personal_best = p[i].current;                                                                                                     
		v[i] = 0;                                                
	}
}

void cpso_sk(){
	int iter = 1;
	clock_t start, end;
	start = clock();
	int particle_num = 100000;
	int split = 1000;
	int count = particle_num / split;
	for(int i = 0; i < particle_num; i+=count){
		while(iter < Iteration){
			for(int j = i; j < count; j++)
				if(fitness(p[j].current) < fitness(p[j].personal_best))
					p[j].personal_best = p[j].current;
			for(int k = i; k < count; k++)
				if(fitness(p[k].current) < fitness(global_best))
					global_best = p[k].current;
			for(int u = i; u < count; u++){
				v[u] =X_const * (v[u] + C1 * rand1() * (p[u].personal_best - p[u].current) + C2 * rand1() * (global_best - p[u].current));
				if(v[u] > VMAX)
					v[u] = VMAX;
			}
			for(int j = i; j < count; j++)
				p[j].current += v[j];
			iter++;
		}
		end = clock();
		time_pso = end - start;
	}
}

int main(){
	init();
	cpso_sk();
	cout<<"The cpso algorithm use "<<time_pso<<" in the funtion 1 and the global best is "<<global_best;
	return 0;
}



```
