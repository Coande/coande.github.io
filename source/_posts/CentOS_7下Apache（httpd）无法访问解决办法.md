title: CentOS 7下Apache（httpd）无法访问解决办法
tags:
  - CentOS
  - Linux
id: 336
categories:
  - 技巧
date: 2015-07-08 17:07:33
---

虚拟机里的CentOS 7安装的Apache（httpd），yum方式安装过了，源码包方式也安装过了。本来是想检测软件是否安装成功的。在主机里访问虚拟机，压根不能访问。后来查相关资料得知是防火墙问题。<!--more-->

运行下面一条命令即可把tcp的80端口设置成允许任何IP都可以访问：
```
[root@localhost ~]# iptables -I INPUT -p TCP --dport 80 -j ACCEPT
```
然后在主机就可以正常访问了。要让其它端口设置成允许任何IP都可以访问只需更改上命令中的80为其它端口即可。需要注意的是使用这种方法重启后还得重新执行一次。

如果用只是自己学习用，可以切底关闭firewall防火墙（仅适用于CentOS 7）：
```
#停止firewall
systemctl stop firewalld.service
#禁止firewall开机启动
systemctl disable firewalld.service
```

<br />
*参考了：*
[centos7 关闭firewall安装iptables并配置](http://linux.it.net.cn/CentOS/fast/2015/0110/11567.html)