title: Java中使用equals时的注意事项
tags:
  - Java，equals
id: 297
categories:
  - 技巧
date: 2015-06-08 15:38:11
---

使用equals进行比较的时候，如果要将`String`与`int`类型数据进行*比较*，应该先将int型数据转换成String再进行比较，否则，看起来虽然内容相同，但是返回的总是false！<!--more-->

代码如下：
```
String s=1;
int i=1;
s.equals(i); 	//返回false
```
```
String s=1;
int i=1;
String s2=i+""; 	//将int型数据转换成String，双引号中间没有空格喔
s.equals(s2); 	//返回true
```