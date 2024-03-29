title: 地腿（LandLeg） Java版
date: 2016-04-16 17:21:50
tags: 
	- LandLeg
	- 天翼
categories:
	- 作品
---
LandLeg Java版低调发布，这个版本是根据**XenK0u**的地腿php版移植并增强的，灰常感谢**XenK0u**。

![LandLeg v1.0](http://qiniu.e12e.com//2016/12/31/784942f4ae3c4657.png)

## 地腿是啥？
广东**\*天\*翼\*校\*园\*第三方客户端。**没有WiFi共享检测，拨号功能增强。
<!-- more -->
<br />
## LandLeg Java版 v1.0
### 功能
- **替代**\*中\*国\*电\*信\***天\*翼\*校\*园\***，拨号上网。
- 拨号一次，即使机器重启也可保持连接状态（IP不改变的情况下）。
- 为路由器拨号。

### 此版本在**XenK0u**的php版本基础上进行了一些增强：
- 若没有在配置文件中填写客户端ip，则自动获取
- 若没有在配置文件中填写客户端mac，则自动获取
- 若没有在配置文件中填写nasip，则自动获取
- 维持连接时间间隔添加到配置文件，方便更改
- 添加退出登录功能，方便测试~


### 简单使用说明
- 首先，得确保有Java运行环境。没有就去[下载安装](http://www.java.com/zh_CN/)。
- 在`account.properties`中填写宽带账号、密码
- 打开`登录.bat`。弹出黑窗口提示登录成功就可以上网了。黑窗口可以关闭，但是关闭后啥时候断网就不知道了，一直开着可以保持连接。
- 某些特殊情况需要断网的，可以打开`登出.bat`来退出登录。

### 高级使用说明
- 参看[LandLeg 使用说明](/2016/05/09/LandLeg-使用说明/)

### 配置文件修改说明
仅适用于v1.0 & v1.1
> \# v1.0版修改`account.properties`文件，v1.1版修改`config.txt`文件
\# 宽带账号（必填）
username=12345678910
\# 宽带密码（必填）
password=12345678
\# 宽带接入服务器的 IP 地址（选填，程序能够自动获取）
nasip= 
\# 客户端 IP 地址（选填，程序能够自动获取）
clientip= 
\# 客户端 MAC 地址（选填，程序能够自动获取）
mac=
\# 维持连接请求发送时间间隔（必填，但默认30即可，单位：分钟）
time=30

### 其它
程序在登录成功时，会发送一个请求到我的服务器进行简要统计，会带上md5加密后的mac地址和所在城市信息，希望不要介意哈∩_∩


## LandLeg Java版 v1.1    2016/4/18更新
- 附上一个带jre的版本，即不用自己配置Java运行环境，可以直接使用，但体积比较大，你懂的。
- 配置文件名称由`account.properties`更改为`config.txt`，便于小白进行修改←_←。
- 程序打印更多信息，如自动获取的ip地址信息，便于查错。


## LandLeg Java版 v2.0		2016/5/8更新
- 配置中添加是否自动设置nasip、clientip等的开关。方便高级功能和基本功能的切换使用。
- 登录后不再重写配置文件。自动获取的IP地址等信息不再写入用户配置文件中，下次登录不再需要更改配置文件。
- 若干代码改动，优化逻辑~~so，版本号直接上2.0了。

## LandLeg Java版 v2.1		2016/9/11更新
- 添加维持连接失败后自动重连功能。


## 更多
终于码完了~ 如果觉得不错，点[这里](/others/aboutMe/)鼓励一下我，让我做得更好。




<br />
**Tips**：
~~[LandLeg Java版 v1.0 By Coande下载](http://pan.baidu.com/s/1dF6qlpR)~~
~~[LandLeg Java版 v1.1 By Coande 下载](http://pan.baidu.com/s/1pLkXj6N)~~
~~[LandLeg & JRE 版 v1.1 By Coande 下载](http://pan.baidu.com/s/1nuOG8D7)~~
~~[LandLeg Java版 v2.0 By Coande 下载](http://pan.baidu.com/s/1c7dwLo)~~
~~[LandLeg & JRE 版 v2.0 By Coande 下载](http://pan.baidu.com/s/1i5JGvy9)~~
~~[LandLeg Java版 v2.1 By Coande 下载](https://pan.baidu.com/s/1jI2Qt1s)~~
~~[LandLeg & JRE 版 v2.1 By Coande 下载](https://pan.baidu.com/s/1c64zy2)~~

**全军覆没，默哀。。。**

~~[LandLeg Java版 源码](https://github.com/Coande/LandLeg_Java)~~

~~[LandLeg php版 By XenK0u](http://henbukexue.science/blog/?id=46)~~
~~[LandLeg Python版 By XenK0u](http://henbukexue.science/blog/?id=47)~~



