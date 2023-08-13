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

​![](http://qiniu.e12e.com/default/20230814014404.png)  
​![](http://qiniu.e12e.com/default/20230814014521.png)​  
​​![](http://qiniu.e12e.com/default/20230814014649.png)​​

## 操作：

* IntelliJIdea 分别使用各个选项进行 Git Reset 到 commit b
* 记录结果

## 结果

### Soft

​![](http://qiniu.e12e.com/default/20230814014703.png)  
​![](http://qiniu.e12e.com/default/20230814014713.png)​

### Mixed

​![](http://qiniu.e12e.com/default/20230814014726.png)​

​![](http://qiniu.e12e.com/default/20230814014734.png)​

## Hard

​![](http://qiniu.e12e.com/default/20230814014753.png)​

​![](http://qiniu.e12e.com/default/20230814014806.png)​

### Keep

​![](http://qiniu.e12e.com/default/20230814014813.png)​

​![](http://qiniu.e12e.com/default/20230814014824.png)​
