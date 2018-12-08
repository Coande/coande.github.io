title: 记JavaScript的一次教训
date: 2015-08-20 01:04:13
tags:
categories:
---
这是个集合的遍历问题。代码看上去没有问题，但它的确存在问题，元素总是遍历不完全。我这次的情况就是“点击保存”更改后无法完全处理`input`标签。被这个问题困扰了很久，四处求解才得以解决了，记一下。
错误事例页面：[打开页面](/others/记JavaScript的一次教训/记JavaScript的一次教训-错误事例.html)
修正后：[打开页面](/others/记JavaScript的一次教训/记JavaScript的一次教训-修正后.html)

了解得知，这个错误大概是由于集合的动态变化引起的。

<br />
**Tip**：
在JS中`getElementsByTagName()`获得的是一个类似于数组的`NodeList`对象，但除了有个`length`属性和下标取值以外再也没有别的数组方法了，因为他不是一个真正的数组对象。[@Trinx *on CSDN*](http://my.csdn.net/mawentao728)

[getElementsByTagName返回的是一个数组吗?](http://www.blogbus.com/abaper-logs/29989141.html)