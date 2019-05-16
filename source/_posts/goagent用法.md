title: goagent用法
tags:
  - 翻墙
  - goagent
  - VPN
  - 代理
id: 212
categories:
  - 技巧
date: 2015-04-04 20:30:35
---

今天没事干，又来玩玩goagent，顺便写写。<!--more-->（[goagent是什么？](http://zh.wikipedia.org/wiki/GoAgent "点此查看维基百科")）

一年多没用上goagent了，前段时间我也下载了个，直接在360浏览器里设置代理，但是没设置好，翻不出去。当时我就以为goagent失效了，加之在某群里有人说goagent被和谐了，我真的以为被和谐了，然后就罢休了。但是，昨天在另一个群里我又听说goagent没有被和谐，还说一直在用goagent，我抱着希望继续折腾……

我首先试了在360浏览器里设置代理，还是是不行……后来我又找了几篇教程，乱撞乱撞，终于翻出去了。我总结一下：不能在360安全浏览器工具里设置代理可以这样：右键点击任务栏的goagent，在菜单中选择“设置IE代理”，选择8086或者8087端口的就行了（默认是禁用代理），然后对浏览器设置使用IE代理设置（工具>代理服务器>使用IE代理设置”）。这样设置的的话是对IE的代理进行了设置（大部分软件都是使用IE的代理设置）。

* * *

上面废话，现在正式步入正题：
1. 要使用goagent的需要有一个google账号（这一步就难倒你了？[VPN](http://www.e12e.com/2015/01/30/一些小技巧（持续更新）/ "VPN就在其中")|[浏览器](http://www.e12e.com/2015/03/21/翻墙浏览器全平台版本（windowsandroidiphoneipad-hd）/ "借用一下别人配置好的goagent浏览器")|[Google注册](https://accounts.google.com/SignUp?continue=https%3A%2F%2Fwww.google.com.hk%2F&amp;hl=zh-CN "去注册个Google账号")）
2. 注册好后设置一下账户。将两部验证设置为停用，不够安全的应用访问权限设置为以允许。
![账户设置](http://qiniu.e12e.com/2015/04/04/账户设置.png)
3. 到GAE（Google App Engine）创建应用（Create Application），网上很多人说要验证手机号，反正我不用（注册的时候填写了个手机号，填写了个邮箱，但是不用进行验证）。
 1. 填写Application Identifier，即appid，配置goagent的时候用到，然后Check Availability。（提示一下，invalid是无效的意思，appid的长度必须在6-30个字符之间，且不能使用大写字母，第一个字符必须是个字母）。
 2. 填写Application Title，随便填写。
 3. 下面的设置不用管，直接Create Application即可。可以重复以上步骤创建多个应用得到多个appid（对goagent设置多个appid貌似可以更稳定一点吧）。
![创建应用](http://qiniu.e12e.com/2015/04/04/创建应用.png)
4. 到github下载goagent（当然，里面也有更详细的教程和各参数解释等等。[点此直达](https://github.com/goagent/goagent "去下载goagent")）。
5. 下载到的goagent解压出来goagent文件夹下会有两个文件夹，分别是local（本地使用）和server（服务器端使用）。
6. 进入“server”文件夹，打开“uploader.bat“，按提示操作即可。
 1. 首先输入appid（即第3步提到的appid，输入第3步填入的id即可），多个appid使用”|“隔开即可。
 2. 输入Google账户的Email。
 3. 输入Google账户的密码。
![上传过程](http://qiniu.e12e.com/2015/04/04/上传过程.png)
![上传成功](http://qiniu.e12e.com/2015/04/04/上传成功.png) 上传成功[/caption]
 4. 直到提示上传完成。至此，server文件夹基本用不上了。
7. 进入”local“文件夹，找到”proxy.ini“文件，右键使用记事本打开，编辑一下”[gae]“下的appid即可。appid等于号后面填上刚才第6步上传了的goagent的appid，多个appid也是使用“|”隔开。
![设置gae](http://qiniu.e12e.com/2015/04/04/设置gae.png)
（提示：第6第7步可以看成完全不相关的两步，反正你第7步设置的appid确保是上传成功的即可。所以，只要appid不去设置限制，你的appid也可以和别人分享，你也可以使用别人的appid，那些翻墙浏览器大概也是这样子的吧……）
8. 然后，右键“以管理员运行”来打开“local”文件夹下的“goagent.exe”。以管理员身份运行的作用是导入证书，导入后就不用再使用管理员身份运行了。当然，你也可以手动导入证书，这里就不说了，可以自己参考github上的教程。
9.goagent运行起来了，右键托盘图标选择“设置IE代理”，8086或8087端口的都可以。其中8086是使用goagent自带的规则去访问网站，即需要翻墙才能访问的网站会自动翻墙，不需要翻墙都能访问的网站就会直接连接而不使用代理，百度搜索“ip”看到的是你的当前地点；8087是全局使用代理，即访问的所有网站都使用代理进行访问，百度搜索“ip”看到的是“美国”。8088貌似是PHP的goagent，我也不懂……这里设置的是IE的代理，很多软件都是使用IE的代理设置，所以其他浏览器一般都是能够通过代理的，火狐浏览器就不行的了。不需要翻墙了记得将其设置成“禁用代理”，否则你的IE代理设置还是使用goagent，而goagent却没有启动起来就导致上不了网。
![设置IE代理](http://qiniu.e12e.com/2015/04/04/设置IE代理.png)
* * *

至此，goagent已经基本设置成功了。至于怎样知道是否设置成功，你可以打开IE（推荐用IE试下），打开一个被墙的网址（[可以点我](https://www.youtube.com/ "YouTube")）就知道了。

![YouTube](http://qiniu.e12e.com/2015/04/04/YouTube.png)


至于更深一层的设置在这里就别说了，简单才是这篇博文目的，如有需要可以自己到github上查看详细教程。goagent在github的主页地址：[https://goagent.github.io/](https://goagent.github.io/ "去看看goagent详细信息")


**Tips：**goagent有流量限制（貌似是每个appid限制1G/天），所以你要看视频的话建议使用多个appid。


2015/4/9更新：一段时间后，goagent可能会出现一大片黄绿色的字，这应改是因为goagent配置文件中一大堆原来可用的Google的ip现在不可用了，你有耐心的话可以等等看（它会自动测试一大批ip），没耐心的话你有两个选择：1.到网上找Google可用ip（可以利用一些工具，自己找），然后替换掉；2.使用goagent的php模式，详细设置方法请看另一篇博文：[goagent的php模式](http://www.e12e.com/2015/04/09/goagent的php模式/ "去看看")。