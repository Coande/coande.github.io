title: LandLeg 使用说明
date: 2016-05-09 16:20:13
tags: 
	- LandLeg
categories:
	- 技巧
---
此说明适用于**LandLeg_Java v2.0**和**LandLeg_Android v1.0**

<!-- more -->

## Java版
### 为本机拨号
1. 修改配置文件。
用记事本打开`config.ini`文件，在`user=`后填写宽带账号，在`password=`后面填写宽带密码。
2. 运行`连接.bat`进行宽带连接。

### 为路由器拨号

1. 路由器配置。
    1. 登录路由器后台， `WAN`口连接类型设置为`动态IP`，保存。
    2. 等待`WAN`口获取到IP、网关、DNS等信息，记录下来。
    2. 修改`WAN`口连接类型为静态IP，填入刚才记录下来的IP、网关、DNS等信息，保存。
2. 修改配置文件。
    1. 用记事本打开`config.ini`文件，按要求填写宽带账号和密码。
    2. `isauto`修改为`0`，即设置成手动。
    3. 填入记录下来的`IP`、`MAC`（可以在路由器的状态信息中查看）。
    4. 查看`NASIP`。未拨号情况下，随便访问一个网页会自动跳转到天翼校园网，查看地址栏如：http://enet.10000.gd.cn:10001/qs/index.jsp?wlanacip=xx.xx.xx.xx&wlanuserip=10.23.57.36，其中`wlanacip=`后面的`xx.xx.xx.xx`即为NASIP地址。
    5. 填入`NASIP`。
3. 运行`连接.bat`进行宽带连接。

注意，`isauto`设置为0时，必须填写IP、MAC、NASIP等信息。

## 安卓版
和Java版的大同小异，略。

注意，`启用高级设置`打勾时，可以为路由器拨号；不打勾时，可以为本机拨号。


## FAQ
- 为什么要为路由器设置成静态IP？
方便下次拨号。如果不设置成静态IP，下次路由器断电后IP可能会发生改变，又要更改配置文件。同样，自己的电脑也可以设置成静态IP，然后下次可以使用安卓版的LandLeg来拨号。

- 获取NASIP失败？
    - Java版可能原因：
        - 所在区域不支持天翼校园客户端
        - DNS没有设置成自动获取
        - 宽带已连接
    - Android版可能原因：
        - 所在区域不支持天翼校园客户端
        - 没有连接上天翼校园的WIFI网络
        
- 是否需要关闭路由器的DHCP功能？
不需要！关闭DHCP功能后需要手动设置IP地址。

- Java版能否启动时不要显示黑窗口而后台运行？
Windows系统下可以（带JRE版不行，请下载不带JRE版）。只要用记事本打开`连接.bat`编辑，将`java -jar .\Program\Connect.jar`中的`java`改成`javaw`，即改成`javaw -jar .\Program\Connect.jar`，然后运行`连接.bat`就没有任何提示了。若要关闭，可以打开任务管理器进行关闭。


<br>
**Tips：**
[地腿（LandLeg） Android版](/2016/05/01/LandLeg-Android/)
[地腿（LandLeg） Java版](/2016/04/16/LandLeg-Java/)