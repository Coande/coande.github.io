---
title: Git Reset 各选项的区别
updated: '2023-08-13'
excerpt: ''
permalink: /post/the-difference-between-the-options-of-git-reset-znt8jl.html
comments: true
toc: true
---



<div>
<!-- more -->
</div>

## 初始文件和状态：

* commit a: file a
* commit b: file b
* commit c: file c
* staged: file d

​![img_15](assets/img_15-20230814000822-4nrfncd.png)  
​![img_6](assets/img_6-20230814000841-g5lgebi.png)  
​![img_5](assets/img_5-20230814000849-cutdid3.png)​

## 操作：

* IntelliJIdea 分别使用各个选项进行 Git Reset 到 commit b
* 记录结果

## 结果

### Soft

​![img_12](assets/img_12-20230814000946-tocwhkj.png)  
​![img_11](assets/img_11-20230814000955-ge6645y.png)​

### Mixed

​![img_9](assets/img_9-20230814001007-4k4k3e5.png)  

​![img_10](assets/img_10-20230814001022-bio7ggt.png)​

## Hard

​![img_13](assets/img_13-20230814001033-16pj1ze.png)  

​![img_14](assets/img_14-20230814001041-cl6fcu3.png)​

### Keep

​![img_1](assets/img_1-20230814001050-inc98vt.png)  

​![img_3](assets/img_3-20230814001059-5marxeh.png)​
