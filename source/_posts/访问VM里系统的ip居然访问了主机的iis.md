title: 访问VM里系统的ip居然访问了主机的iis
tags:
  - WAMP
  - 网络配置
  - 虚拟机
id: 347
categories:
  - 技巧
date: 2015-07-10 23:59:51
---

今天在虚拟机的window7中安装了个wamp，想在主机上测试是否能够访问。但是，输入我虚拟机里window7的ip后居然发现访问的是自己主机上的iis服务器上的内容。<!--more-->虚拟机里和主机能相互ping通；我对照了ip，没输入错ip啊；看了下主机网络连接里的VMnet8（我的VM网络用的是NAT模式），设置也没问题；主机上访问一下VM里的一个Linux的Apache，能正常访问那个Apache的页面；换了其它浏览器，清空了缓存，访问VM里面的这个win7的ip依然是直接访问到了我主机上的iis上的页面；直接输入ip的，那又不关hosts的事。是不是很奇怪？

无奈了，快要绝望的时候，然后将网络连接里的每个连接都仔细看看ip设置有没有问题……

当看到VMnet1的时候，突然觉得世界变得美好了（大概是兄弟连某某老师的一句话^\_^），原来这里的ip也设置成和虚拟主机的里win7的ip相同了……立马改掉，顺便将它禁用掉╰\_╯。