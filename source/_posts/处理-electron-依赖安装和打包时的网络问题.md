---
title: 处理 electron 依赖安装和打包时的网络问题
date: 2019-06-07 23:58:28
tags:
---

网上搜的给 npm 配置淘宝镜像，设置 `ELECTRON_MIRROR` 变量等，实测无效。最后是如下方法解决的：

<!-- more -->

缺什么文件就手动下载什么文件：

```
// 淘宝镜像：
https://npm.taobao.org/mirrors/electron/<版本号>/
// 或者 github：
https://github.com/electron/electron/releases/tag/v<版本号>
```

下载完，拷贝到 electron 的缓存文件夹中即可。

windows 下缓存文件夹：

```
C:\Users\<用户名>\AppData\Local\electron\Cache
```

Mac 下缓存文件夹：

```
/Users/<用户名>/Library/Caches/electron
```





以上参考：[Installation](https://github.com/electron/electron/blob/master/docs/tutorial/installation.md)

附上今天打包的：[iptv-m3u-player 电视直播软件](https://github.com/Coande/iptv-m3u-player)