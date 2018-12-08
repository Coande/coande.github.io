title: Fiddler抓取手机数据
tags:
  - Fiddler
  - 抓取手机数据
id: 199
categories:
  - 技巧
date: 2015-03-22 15:21:35
---

Fiddler抓取手机数据也是很简单的。只需简单几步设置即可：<!--more-->

**电脑端设置：**
1. 在Fiddler菜单中选择Tools/Fiddler Options…。
2. 在弹出窗口中选择Connections标签。
3. 对“Allow remote computers to connect”打上勾。
4. 重启Fiddler。
5. 电脑开热点（[这都不会？](http://wifi.liebao.cn/)）。
6.  快捷键win+r输入cmd运行命令行后输入ipconfig查看此热点对应的无线设备的ip地址，记下来等会要用。
![Fiddler Options](http://7xi6qe.com1.z0.glb.clouddn.com/2015/03/22/20150322143312.png)

![Connections](http://7xi6qe.com1.z0.glb.clouddn.com/2015/03/22/connections.png)

![ipconfig](http://7xi6qe.com1.z0.glb.clouddn.com/2015/03/22/ipconfig.png)

手机连接上电脑发出的热点后，需要在手机端对其进行设置。

**手机端设置：**

1. 手机端对WiFi设置代理。其中的代理设置为手动，主机名为刚才记下来的IP地址，端口号填上Fiddler的默认端口号8888。
2. 保存后即可在电脑上抓取到手机端数据。
![WiFi列表](http://7xi6qe.com1.z0.glb.clouddn.com/2015/03/22/Screenshot_2015-03-22-14-35-24.png)
![设置代理](http://7xi6qe.com1.z0.glb.clouddn.com/2015/03/22/Screenshot_2015-03-22-14-35-56.png)


**注意：**抓完手机端数据后最好关掉手机端WiFi设置的代理（将代理设置回“无”），以免日后手机连接此WiFi出现网络问题。

**Tips：**点击关闭Fiddler左下角的capturing后就可以只抓取手机端数据而不会抓取电脑端的数据。