title: goagent的php模式用法
tags:
  - 翻墙
  - goagent
id: 228
categories:
  - 技巧
date: 2015-04-09 17:44:11
---

前几天的一篇文章介绍了如何设置goagent。但是，我那天设置好的goagent现在又有点问题了（打开goagent一段时间后才能正常使用，原因应该是因为大部分ip失效了，换过一些可用ip即可，至于怎样获得这些ip，我就不说了，自己百度~）。说下不需要经常更新ip也可以照样能够翻墙的方法，goagent的php模式翻墙。<!--more-->


下面简单说说整个过程：

1. 上传goagent的server/php目录下的index.php（relay.php不用上传）到虚拟主机（虚拟主机管理页面上传或使用FTP工具上传）。

2. 设置goagent的local目录下的”proxy.ini“文件。修改[php]下的enable值改为1（启用的意思），fetchserver就改成自己的自己虚拟主机上goagent的那个php文件的路径，例如：http://www.e12e.com/index.php

3. 打开goagent，右键goagent托盘图标设置IE代理为端口为8088的那个就OK了。

至此，php模式的goagent设置完成了。

goagent的这种模式设置起来也很简单，我也懒得详细写了，详细的可以去**山猫的博客**看看：[点此直达](http://shanmao.me/webservice/windows/shi-yong-goagent-rang-php-kong-jian-bian-cheng-ni-de-zhuan-shu-dai-li-fu-wu-qi-ji-yu-php-kong-jian-zi-jian-dai-li)。
* * *

**常见问题：**

- 我怎么知道虚拟主机支不支持这种模式？
试了就知道嘛。

- 这种模式的优点？
这种模式运行就和GAE就没有关系了，免去了appid，访问的网站都是通过你的虚拟主机作代理来访问的，即”你的电脑--&gt;虚拟主机--&gt;网站“，百度”ip“得到的是你虚拟主机的ip地址，所以有个要求就是虚拟主机必须不在大陆。我觉得这种模式的goagent应该算是一个VPN了。

- 用完goagent后上不了网？
再次打开goagent，然后右键goagent的托盘图片设置IE代理为禁用即可。还有一种方法是：打开IE，打开”Internet选项“，在”连接“标签下的“拨号和虚拟专用网络设置”左侧选择你的网络连接类型（有一个或多个的，不清楚是哪种的话全部按后面设置一遍），对其进行“设置”，有打勾的选项全部取消掉，然后“确定”返回到“连接”标签，还需要对“局域网（LAN）设置”，也是把所有的勾去掉即可。
