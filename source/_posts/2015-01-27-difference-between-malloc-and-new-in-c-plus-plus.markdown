---
layout: post
title: "difference between malloc and new in C++"
date: 2015-01-27 15:30:52 -0500
comments: true
categories: c cplusplus
---

###new and delete
- the way it allocate and release memory
	- the memory is allocate from `Free Store`
	- will return a fully typed pointer
		- if failed will not return NULL
	- the compiler will calculate the size
	- reallocate is not handled intuitively, using copy constructor
	- whether called malloc and delete can be user defined
	- can add a new memory allocator to deal with low memory
	- new and delete can be overwrite legally
	- use constructor/destructor to initial/destory object
<!--more-->
- new 动态创建和释放数组或者单个对象
	- 动态创建对象的时候，只需要指定其数据类型，不必为该对象命名
	- 如果分配失败了，会抛出异常。
	- new 表达式返回指向该新建对象的指针
	- 我们可以通过这个指针来访问新建的对象
	- int *p = new int
		- 返回类型为int*类型， 分配大小为sizeof(int)
	- int *p = new int[100]
		- 返回类型为int*类型, 分配大小为sizeof(int) * 100


- 三种特殊指针
	- void* 表示未确定类型的指针，更明确的说是指申请内存空间时还不知道user是用来储存什么类型的数据的。
	- 零值指针：值为0的指针。可以是任何一种指针类型。
	- NULL指针：不提供任何地址信息的指针

- new 动态创建的对象是可以初始化的。
	- e.g int *p = new int(1000)
	- 如果不初始化，就会使用这个类的默认构造函数来初始化。
		- e.g int *p = new int()  //初始化为0
	- 但是如果对象是内置的，就没有初始化
		- e.g int *p = new int //指向一个没有初始化的int
			- string *str = new string()  //初始化为空串，因为string自带的默认构造函数会初始化为空串

- delete
	- delete p; 
		- 但是释放完p的内存之后，p会变成不确定的指针
		- 因此要把p赋值为0
			- 明确指针不再指向任何对象

###malloc and free
- the way it allocate and release memory
	- the memory is allocate from `Heap`
	- will return a void pointer 
		- will return NULL if failed
	- the space and size need to be specified(固定)
	- will not called new/delete
	- it is simple to reallocate large memory
	- user can not write code into allocation sequence to help with low memory
	- malloc/free can not be overriden legally

- malloc 动态内存分配
	- void *malloc(int size)
	- 向系统申请分配指定size个字节的内存空间
	- 申请之后要检查是否分配成功
	- 不用之后要释放：把纸箱这块内存的指针指向NULL, 防止程序不小心使用了它
		- 如果忘了释放就是内存泄露
	- 操作系统中有一个记录空闲内存位置的链表，每次收到程序申请的时候，就会遍历这个链表，找到第一个空间大于申请的空间的堆节点，然后把该节点从链表中删除，把这个节点的空间分配给程序。
	-  int p;
		- p = (int*)malloc(sizeof(int) * 128)
		- p指针会存储存储单元的首地址
