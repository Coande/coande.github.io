title: webmin某错误提示解决方法
tags:
  - Linux
  - webmin
id: 384
categories:
  - 碎片
date: 2015-07-11 18:43:36
---

Webmin是一个基于Web的Linux系统管理界面。你就可以通过图形化的方式设置用户账号、Apache、DNS、文件共享等服务。安装完成并登录后却提示：Require package-updates/install_check.pl failed : Died at (eval 149) line 1。（eval后的数值可能会不同）<!--more-->

![Require package-updates/install_check.pl failed](http://7xi6qe.com1.z0.glb.clouddn.com/2015/07/11/2015-7-11_18-40-46.png)

解决方法：
```
[root@localhost cdrom]# yum install perl-Data-Dumper
```
安装个perl-Data-Dumper即可。