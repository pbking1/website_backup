---
layout: post
title: "string processing function implementation"
date: 2015-04-21 01:56:01 -0400
comments: true
categories: c++
---
###string function in c
####strcpy
- 使用一个临时变量保存串的首地址，然后最后返回这个地址
- 然后在最后判断是否遇到'\0'来结束复制
```
char *strcpy1(char *des, const char*src){
	char *address = des;
	while((*des++ = *src++) != '\0');
	return address;
}
int main(){
	char *des;
	char *src = "aaa";
	char *result;
	result = strcpy1(des, src);
	cout<<result;
	return 0;
}
```
--------------------------------------

####strlen
- 一直累加直到判断是否遇到'\0'来结束计数
```
int strlen1(const char*src){
	int count = 0;
	while((*src++) != '\0')
		count++;
	return count;
}
int main(){
	char *src = "aaa";
	int result;
	result = strlen1(src);
	cout<<result;
	return 0;
}
```

--------------------------------------

####strcat
- 把指针移到最后，然后把b字符串的内容复制到a字符串最后
- 但是要注意a字符串要有足够的空间来支持b字符串内容的大小
```
char *strcat1(char *des, const char*src){
	char *address = des;
	while(*address)
		address++;

	while((*address++ = *src++) !='\0');
	return des;
}
int main(){
	char des[10] = "";
	char *src = "aaa";
	char *result;
	result = strcat1(des, src);
	printf("%s", result);
	return 0;
}
```
--------------------------------------

####strcmp
- 如果字符串一样，那么返回0
- 如果a>b那么返回正数，否则返回负数
- 比较方法是用asc码来比较，然后最后返回相减的结果
	- 从左到右比较，知道出现不一样的字符或者出现'\0'为止
```
int strcmp1(const char *s1, const char*s2){
	while(*s1 == *s2){
		if(*s1 == '\0'){
			return 0;
		}
		++s1;
		++s2;
	}
	return *s1 - *s2;
}
int main(){
	char *des = "aaa";
	char *src = "aaa";
	int result;
	result = strcmp1(des, src);
	if(result == 0)
		cout<<"the string are the same";
	else
		cout<<"the string are not the same";
	return 0;
}
```
