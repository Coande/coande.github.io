title: CentOS中安装hping
date: 2015-08-26 23:53:38
tags:
	- Linux
	- hping
categories:
	- 技巧
---
到官网找到`hping`的`github`链接，复制下载地址。`wget 地址`进行下载。
下载下来的文件没有后缀，`file 文件名`查看文件类型得知是zip包。
`unzip 文件名`进行解压，`cd`到`hping`的目录等待下一步操作。<!--more-->

解决安装问题：
`yum install libpcap-devel`安装依赖包`libpcap-devel`。
`yum install tcl-devel`安装`tcl`和`tcl-devel`。
`ln -s /usr/include/pcap-bpf.h /usr/include/net/bpf.h`做个软连接。

进行安装：
`./configure`进行编译前准备。
`make`编译生成二进制文件。
`make strip`然后`make install`进行安装。

<br />
CentOS中安装hping遇到的错误：
1. **libpcap_stuff.c:19:21:致命错误：net/bpf.h：没有那个文件或目录**
解决方法：ln -s /usr/include/pcap-bpf.h /usr/include/net/bpf.h

2. **/usr/bin/ld: cannot find -ltcl**
解决方法：yum install tcl-devel

3. **NO TCL scripting support compiled in**
解决方法：make strip

<br />
**Tip**：
[hping官网](http://www.hping.org/)
[hping *on GitHub*](https://github.com/antirez/hping)