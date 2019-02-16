---
title: 对cookie操作的误解
date: 2019-01-16 10:50:58
tags:
---
`document.cookie`可以读取到非httponly属性的cookie。httponly属性的cookie只能服务器端读取，浏览器脚本不允许直接读取。

`document.cookie`可以读取到n个cookie信息，理所当然的也会认为`document.cookie`也就是普通一个字符串变量而已，设置cookie也就直接n个cookie拼成字符串赋值回去覆盖。实际测试其实并不是这样的，设置cookie，需要一个一个cookie分别设置：

<!-- more -->

```
// 错误写法，只能设置 a=1 这个cookie
document.cookie = 'a=1; b=2';

// 正确写法，要一个一个cookie分别设置
document.cookie = 'a=1';
document.cookie = 'b=2';

// 这时的cookie实际上为："a=1; b=2"
console.log(document.cookie);
```


**Tips：**
[Edit-This-Cookie](https://github.com/ETCExtensions/Edit-This-Cookie)