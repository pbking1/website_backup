---
layout: post
title: "2014 sysu database project step1"
date: 2014-05-13 15:20:32 +0800
comments: true
categories: database
---

###问题描述
- **任务 1: 不带压缩地导入数据**
	- 这个任务要求你实现分页存储机制。
		- 此处仅考虑定长的数据类型。对于每一列,需要将所含的定长数据如同数组 一样存储在磁盘上的页中 (更多解释见下文)。每一页的大小是固定的,可以是 4K,8K 或 16K。
	- 在这个任务中,你需要存储 ORDERS 表中的
		- 1.O_ORDERKEY
		- 2.O_CUSTKEY
		- 3.O_TOTALPRICE 
		- 4.O_SHIPPRIORITY
	- 不同列的数据类型不一样,具体请参考 TPC-H 的文档。存储之后,你需要 提供接口,以便于查询记录。查询时,要求实现给定一条记录的 ORDERKEY, 返回这条记录的 CUSTKEY,TOTALPRICE 和 SHIPPRIORITY。
 	- 查询接口的具体要求,请参考提交一节。
	- 这个存储系统必须有能力处理 1G 以上的数据。允许存入内存里的页的数量 为 128。在实现这个限制之外,可以尝试其他限制并做对比。你可能需要学习 LRU 等换页机制来加速数据导入。
<!--more-->
- **任务 2: 外排序和 RLE 压缩**
	- 本任务要求使用行程长度编码 (Run-Length Encoding) 方式压缩数据,并 将 ORDERS 表和 CUSTOMER 表以 CUSTKEY 进行 JOIN 操作。在进行压 缩前,需对数据做外排序 (见下文说明)。

###存储结构
- 请注意在这个项目中,磁盘的读写操作都必须以二进制模式进行。
- 对于一个页,由于数据定长,一列可以以数组形态存在于内存中。例如,按照以下形式声明的数组,
	- `int page[1024]`
	- 可以表示一个大小为 4K 的页。使用以下代码,可以将一页写出, `fwrite(page, sizeof(int), 1024, f)`;
 	- 以上代码仅供参考。具体实现时可能情况更为复杂。
- 对于一个未压缩的页,数据按如下方式按顺序排列,需要读取指定数据时, 通过下标取出对应位置的数据。
	- `<Val1><Val2><Val3><Val4>...`
- 对于压缩的页,则按如下方式排列在数组中。请先自行学习行程长度编码。
	- `<Val1><RunLength1><Val2><RunLength2><Val3><RunLength3>...`
- 一页可以是 4K,8K 或 64K。

###外排序
- 在做 JOIN 之前,需要进行外排序。
	- 简单地说,需要先分别读进每 128 页 进行排序,得到一个个顺串。然后同时对所有顺串进行归并,归并后的结果即 为排好序的数据。请参考维基百科上的说明自行学习和实现。
- 外排序需要同时处理 ORDERS 表的 CUSTKEY 列和 ORDERKEY 列,按照 CUSTKEY 进行排列,如下图所示,
- 排完序后,CUSTKEY 的连续重复项更多了,即可对该列进行 RLE 压缩。 完成压缩后,请统计压缩效率。
- {% img /images/database2014pro/1.png %}

###step1 code

```
#include<iostream>
#include<fstream>
#include<string>
#include<algorithm>
#include<cstdlib>
using namespace std;

struct database_attr{
	int orderkey;
	int custkey;
	int totalprice;
	int prior;
};
database_attr p[1024];

int main(){
	fstream fin;
	char buf[200];
	string str[10][1001];
	string data[5][1001];
	int data1[5][1001];
	int data2[5][1001];
	fin.open("store_test.tbl");
	int row = 0;
	int col;
	int n = 9;
	while(!fin.eof()){
		row = 0;
		fin.getline(buf, 200, '\n');
		for(int i = 0; buf[i] != '\0';){
			if(buf[i] == '|' && n > 0){
				row++;
				i++;
				n--;
			}else if(buf[i] != '|' && n > 0){
				str[row][col] += buf[i];
				i++;
			}
		}
		n = 9;
		col++;
	}
	
	for(int i = 0; i < 9; i++){
		for(int j = 0; j < 1000; j++){
		//	cout<<str[i][j]<<" ";
		}
		//cout<<endl;
	}
	//store the data in column
	for(int i = 0; i < 9; i++){
		for(int j = 0; j < 1000; j++){
			if(i == 0){
				data[i][j] = str[i][j];
			}
			if(i == 1){
				data[i][j] = str[i][j];
			}
			if(i == 3){
				data[i - 1][j] = str[i][j];
			}
			if(i == 7){
				data[i - 4][j] = str[i][j];
			}		
		}
	}
	for(int i = 0; i < 4; i++){
		for(int j = 0; j < 1000; j++){
			//cout<<data[i][j]<<" ";
		}
		//cout<<endl;
	}
	//check the data use the index
	/*
	int ok;
	cin>>ok;
	cout<<data[1][ok]<<" "<<data[2][ok]<<" "<<data[3][ok]<<endl;
	*/
	fin.close();
	//change the string array into int array
	int i, j;
	for(i = 0; i < 4; i++){
		for(j = 0; j < 1000; j++){
			data1[i][j] = atoi(data[i][j].c_str());
		}
	}

	for(i = 0; i < 4; i++){
		for(j = 0; j < 1000; j++){
			data2[i][j] = data1[i][j];
			if(j < 10)
				cout<<data2[i][j]<<" ";
		}
		cout<<endl;
	}
	
	//store the array into struct array
	for(i = 0; i < 4; i++){
		for(j = 0; j < 1000; j++){
			p[j].orderkey = data2[0][j];
			p[j].custkey = data2[1][j];
			p[j].totalprice = data2[2][j];
			p[j].prior = data2[3][j];
		}
	}
		
	cout<<"The id 1 has "<<p[0].orderkey<<" "<<p[0].custkey<<" "<<p[0].totalprice<<" "<<p[0].prior<<endl;
	return 0;
}



```

###step2 code
- to be continued