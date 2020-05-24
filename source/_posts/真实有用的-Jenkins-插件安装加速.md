---
title: 真实有用的 Jenkins 插件安装加速
date: 2020-04-06 16:47:40
tags: Jenkins
---

不论百度还是 Google，搜到 "Jenkins 加速" 方法都太过繁琐且过时。基本上就是那么几种方式：

<!-- more -->

- 修改 Update Site 为[镜像站](http://mirrors.jenkins-ci.org/status.html)
- 修改 Update Site 后由于镜像站中仅做了镜像，部分引用还是引用的 Jenkins 官方站点，所以并不能完全的达到加速效果。然后又有升级版，修改 hosts 实现访问 Jenkins 是访问本地，然后本地搭建一个 nginx 作为代理，把访问 Jenkins 官方站点的请求转发到镜像站上。
- 下载 update-center.json 文件，然后把文件中访问 Jenkins 官方站的请求 URL 修改为 镜像站的 URL，然后开启一个服务，提供 update-center.json，把 Update Site 修改为该文件地址。
- 然后又有人说单纯修改 update-center.json 的话 Jenkins 不认， Jenkins 对 update-center.json 做了签名，还需要替换签名文件……



然后通过 Github 搜索 “Jenkins update”，找到了这个：https://github.com/jenkins-zh/mirror-adapter 。尽管看到 README 中说需要三步：


1. install localization-zh-cn-plugin 1.0.10
2. use the new certificate file
3. change the update center URL


也是需要替换签名文件，但是不需要额外启动一个服务，这也方便不少了呢。但是第二步怎么替换，第三步替换成什么呢也没说清楚~ 那么搜索一下这个 Repository 的名字 “mirror-adapter”，找到好几遍一抹一样的文章，让后顺着找到Jenkins中文社区中的说明，并不需要替换签名文件：

https://jenkins-zh.cn/wechat/articles/2019/11/2019-11-11-update-center-mirror-announcement/

其实最后一句话才是重点，需要安装插件然后设置一下即可。

简单描述一下**操作步骤**：


>1. 安装中文化插件。插件地址：https://plugins.jenkins.io/localization-zh-cn/ 。
>2. 重启Jenkins。可以访问 /restart 来重启。
>3. 设置镜像站地址。点击页面右下角的 “Jenkins 中文社区”，点击“使用”，然后去“设置更新中心地址”，修改升级站点为 https://updates.jenkins-zh.cn/update-center.json 提交，在点一下页面右下角的“立即更新”来更新插件安装地址即可。



设置完后，测试发现基本所有插件都是秒装完。


当然首次使用 Jenkins 时提示安装插件就不要安装了，可以进入后台再按需安装。可能安装中文化插件 localization-zh-cn 时也会很慢，可以借助梯子去 Jenkins 官网搜到该插件及其依赖插件下载下来再上传安装。


> 其实还有一个方法，可以下载国内定制版的 Jenkins：https://github.com/jenkins-zh/jenkins-formulas ，直接把 localization-zh-cn 也安装配置好了。







