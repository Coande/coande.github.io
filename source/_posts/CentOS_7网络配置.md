title: CentOS 7网络配置
tags:
  - Linux
  - CentOS
  - 网络配置
id: 328
categories:
  - 技巧
date: 2015-07-06 14:23:52
---

最近玩玩Linux，用的是`CentOS 7`，`虚拟机`里面安装，没有图形化界面。昨天，当学到RPM包yum在线管理的时候，网络配置难到了我，我自己搞了好久都搞不定，后来请大神帮忙总算配置好了。下面记录一下配置过程和一些方法。<!--more-->
我的CentOS 7，setup里没有ip地址的配置选项了，旧版本的就有，现在唯有动手去修改文件了。我的虚拟机网络连接类型设置为`NAT模式`。

我的网络配置文件为：

	/etc/sysconfig/network-scripts/ifcfg-eno16777736

不同机器，配置文件的名称可能会不同，新版本的一般都这个名称，以前版本的CentOS就叫做`ifcfg-eth0`

首先，打开文件：
```
#用vi打开配置文件
[root@localhost ~]# vi /etc/sysconfig/network-scripts/ifcfg-eno16777736
```
然后，编辑如下参数：

	[code]BOOTPROTO=static
	ONBOOT=yes
	IPADDR0=192.168.88.4
	GATEWAY0=192.168.88.2
	DNS1=114.114.114.114

- BOOTPROTO默认的值为`dhcp`，我们这里使用静态`ip`，所以将其修改为`static`。
- ONBOOT默认的值为`no`，设置的是否在开机时启用该网卡，修改为`yes`。
- IPADDR0为ip地址，填写与主机VMnet8同一网段的ip地址。
- GATEWAY0为网关地址，这个地址可以在VM的菜单栏选“编辑-虚拟网络编辑器”，列表中选择VMnet8，然后在下面选项中选择“NAT设置”，在弹出窗口中即可看到“网关IP”。
- DNS1为DNS：设置下常用的DNS即可（不一定要与VMnet8的DNS相同），可以和我的相同。设置好后保存退出。
```
#重启网络服务
[root@localhost ~]# service network restart
```
然后ping一下，我的就这样通了。配置完成。