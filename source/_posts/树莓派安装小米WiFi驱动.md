title: 树莓派安装小米WiFi驱动
date: 2015-10-06 21:23:05
tags:
	- Linux
	- 驱动
categories:
	- 技巧
---
昨天折腾了一天在树莓派上成功使用小米WiFi。360WiFi，小度WiFi，腾讯WiFi等同样适用。
<!--more-->
教程我不写了，整理一下。

参考资料：[树莓派2安装使用小米WIfi（360 小度 腾讯wifi）](http://www.cnblogs.com/sjqlwy/p/4415935.html)
基本上按照上面的做就是了。需要补充的是：

安装gcc和g++版本为4.8.3+直接跟着这里做就是了：[GCC 4.8 ON RASPBERRY PI WHEEZY](https://somewideopenspace.wordpress.com/2014/02/28/gcc-4-8-on-raspberry-pi-wheezy/)（自备梯子）。但是，我在执行`sudo update-alternatives --remove-all g++`和后面有关`g++`的命令时好像报错了，重启一下树莓派再执行就又通过了。

我在make的时候遇到了个关于“rt_linux.h”的error，前面博客说不用改rt_linux.h文件，我还是改了，改了发现就没有error了。操作方法：打开 include/os/rt_linux.h，找到
```
int fsuid;
int fsgid;
```
并把它改为
```
kuid_t fsuid;
kgid_t fsgid;
```

要将无线网卡设置为静态ip可以参看这里：[Raspberry Pi树莓派无线网卡配置[多重方法备选]](http://www.cnblogs.com/scgw/p/3947980.html)

基本就这些了。操作不是很繁琐，但是很耗时，请耐心等待~

最后说一个悲催的故事，弄了一天才弄好小米WiFi的驱动，睡了一觉醒来想玩玩的时候，网卡彻底坏了~具体原因我不知道~可能是我在通电的时候强拔的缘故，也可能是重启树莓派的缘故，也可能~~~多么的脆弱啊！请慎重！

