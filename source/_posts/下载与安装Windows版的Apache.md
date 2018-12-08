title: 下载与安装Windows版的Apache
date: 2015-08-09 20:39:00
tags:
categories:
---
刚学PHP，要安装个Apache，我就装了~<!--more-->

实际上，也算不上安装，只是添加了个服务罢了。服务不添加也照样可以使用，只是没那么方便。

首先，去[Apache官网](http://httpd.apache.org)找Windows对应的包。结果，Apache的官网并不提供Apache的二进制包，只提供源码包，所以Apache官网上没有。但找到了提供Windws二进制包的第三方网站。官网上有两个版本的Apache，我的目标是稍旧版本的2.2.31，刚开始我也是纳闷了，2.2.31下的栏目里没有“Files for Microsoft Windows”，就在较新版本下的2.4.16下有，才找到官网推荐的几个提供Windows二进制包的下载的第三方网站。推荐的网站有五个，前两个是单独的Apache，后三个是包括Mysql等的集成环境。
![Apache官网1](http://i3.tietuku.com/0ff78a35ce227969.png)
![Apache官网2](http://i3.tietuku.com/5fe2b867a3d7254a.png)
我到[Apache Haus](http://www.apachehaus.com/cgi-bin/download.plx)随便下载了个2.2.31版的Apache后，是一个zip包，贪快，网上查了下用法，然后直接解压里面的`Apache22`到我的常用软件目录“D:\Program Files\”下，然后用命令提示符进入到“D:\Program Files\Apache22\bin”里执行：
```
httpd -k install
```
然后给我个：
```
(OS 5)拒绝访问。  : Failed to open the WinNT service manager
```
其实就是权限不够，无法往系统里添加服务，也就无法使用那个Apache的可视化小工具进行管理。

以管理员身份运行了，但是又给了我一句：
```
httpd: Syntax error on line 35 of D:/Program Files/Apache22/conf/httpd.conf: ServerRoot must be a valid directory
```
当时没注意，忽略了，再运行一次，这次报错是说服务已经安装了。打开ApacheMonitor，start不了，提示请求操作失败。
![Apache操作失败](http://i3.tietuku.com/60da9826ef2ba848.png)
网上查了下，各种答案，看不下去了，下载的zip包里有个`readme_first.html`，还是看看这个吧。看了，说要将Apache22解压到磁盘分区根目录下，然后cmd运行bin下的http.exe测试一下，说没报错而且光标在下一行闪烁就可以正常访问Apache了。我刚开始以为没那个必要将Apache放到分区跟目录下，我就没这样去做。先把刚安装上的服务卸载掉`httpd -k uninstall`，然后直接在cmd里运行了下`httpd.exe`，报错，仔细看了下报错信息，发现有个配置文件的路径需要改改，改完再来运行，又另外一个错，还是路径问题，改了，继续错继续改……改完了发现没报错了。运行后也什么都没提示，可以继续输入命令。浏览器打开输入本地地址，无法访问。不想忙活了~还是按他的文档去做吧，把服务`httpd -k uninstall`卸载了，还是乖乖的把Apache22解压到分区根目录。运行`httpd.exe`，没报错，光标在闪烁，用浏览器访问，正常了。然后再运行`httpd -k install`，也正常执行了，但是有Error字眼：
```
Errors reported here must be corrected before the service can be started.
```
这句话后面没内容了，也就是表示没有Error。

一切搞定了~也可以使用bin下的ApacheMonitor进行管理了。
![IT WORKS](http://i3.tietuku.com/e34625379f3d4f2d.png)
其实，早就应该看readme文件的，而且也应该按照readme去做，也就会避免自己这样瞎折腾了。
<br />
**Tip：**网上也有以软件安装方式进行安装的Apache安装包。

<br />
**更新**：后来看了下注释得知，要更改Apache的安装路径，只需更改`ServerRoot`目录的位置即可。如：
将原本只能将Apache放置在根目录的配置：
```
Define SRVROOT "/"
```
更改为别的路径：
```
Define SRVROOT "F:/workspace/phpEnv/Apache24"
```