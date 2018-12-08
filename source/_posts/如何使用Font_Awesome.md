title: 如何使用Font Awesome
tags:
  - Font Awesome
id: 292
categories:
  - 技巧
date: 2015-06-03 00:44:50
---
由于某维总是说不懂，就写写吧。<!--more-->

首先，得去[Font Awesome官网](http://fortawesome.github.io/Font-Awesome/)下载Font Awesome。

将下载到的zip压缩包解压并复制到你的工程所在路径。

在你的html的`<head>`标签中添加Font Awesom的font-awesome.min.css的引用。如：
```
<link rel="stylesheet" href="path/to/font-awesome/css/font-awesome.min.css">
```
然后，你可以随意加入类似如下的`<i>`标签即可添加对应图标字体（下面对应的是一个相机图标）：
```
<i class=“fa fa-camera-retro”></i>
```
Font Awesome的所有图标字体在这里：[http://fortawesome.github.io/Font-Awesome/icons/](http://fortawesome.github.io/Font-Awesome/icons/)

自己需要什么图标字体就选择什么图标字体点击一下即可看到对应图标字体的`<i>`标签，复制到html中即可。

<br />
**Tips：**这些图标字体可以看作普通字体对其使用css样式，例如改变颜色、背景、位置等等。更多效果可以看这里：[http://fortawesome.github.io/Font-Awesome/examples/#](http://fortawesome.github.io/Font-Awesome/examples/#)