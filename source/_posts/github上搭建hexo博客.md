title: github上搭建hexo博客
date: 2016-02-17 22:06:16
tags:
	- github
	- hexo
categories:
	- 技巧
---
有人叫我教他弄个免费博客。然而，hexo文档看不懂，相关软件又说难下载。所以就写一篇比较傻瓜的教程并附上相关软件，以此也可以加深自己的理解。本文以Windows操作系统为例。

<!--more-->
## 环境安装

**安装Git**
Git：主要用于上传博客页面到github和命令操作
[32位系统点此下载](http://pan.baidu.com/s/1kUo8GiN)
[64位系统点此下载](http://pan.baidu.com/s/1pKs4sLP)
一直next即可。

**安装Node.js**
Node.js：Hexo的运行环境
[32位系统点此下载](http://pan.baidu.com/s/1jHyKlka)
[64位系统点此下载](http://pan.baidu.com/s/1gex4xof)
也是一直next即可。

**安装Hexo**
Hexo：博客程序
打开安装Git后的产生的`Git Bash`，输入（也可以复制粘贴，右键点击标题栏即可弹出选项菜单）：
```
npm install -g hexo-cli
```
回车，需要点时间，耐心等待。


## 生成本地博客
Git bash中输入
```
hexo init myblog
```
初始化博客文件到`myblog`文件夹，其中`myblog`可以根据自己喜好进行修改。

接着输入：
```
cd myblog
```
进入myblog目录，以下所有操作都需要在该目录下完成。下次打开`Git bash`进行操作也需要进入这个目录。

再接着输入：
```
npm install
```
这个命令是安装什么我也不知道~

继续输入：
```
npm install hexo-deployer-git --save
```
来安装将hexo博客向github上传的模块。

最好再输入：
```
npm install hexo-server --save
```
来安装hexo服务器模块，用于本地预览博客

到这里就基本在本地完成博客的搭建了。可以输入如下命令来看下hexo博客的初始效果：
```
hexo s
```
这条命令启动了一个本地的服务器，不要关闭当前`Git bash`窗口，打开浏览器，输入网址`http://127.0.0.1:4000`进行访问。有一篇Hello World博文，效果如下：
![Hexo Hello World](http://i13.tietuku.com/c79155ec31581eb2.png)


## 将本地博客上传到github

**创建github仓库（repositories，其实就是存放博客的地方，相当于虚拟主机）**
要上传到github，首先需要去注册一个github账户：[https://www.github.com](https://www.github.com)。至于怎么注册，这里不多说~
点击右上角的加号：
![新建仓库](http://i11.tietuku.com/7bdf3e392709dad7.png)
Repository Name要按要求填写，如我这里是`jack0416.github.io`，将`jack0416`替换为自己的用户名即可，不区分大小写：
![填写仓库信息](http://i13.tietuku.com/d99c339cdfb071d1.png)

**修改_config.yml文件**
修改`myblog`目录下的`_config.yml`。myblog目录在哪呢？`Git bash`中输入：
```
pwd
```
就会显示当前的目录了，形如：
```
/c/Users/Coande/myblog
```
表示C盘下Users目录，Coande目录，……

找到`_config.yml`文件，用记事本打开（这里推荐安装Nodepad++等第三方文本编辑工具来代替系统的记事本），滚到最下面，修改成：
```
deploy:
  type: git
  repo: https://github.com/Jack0416/jack0416.github.io.git
```
其中，`https://github.com/Jack0416/jack0416.github.io.git`改成你的git仓库地址。git仓库地址查看：
![git地址](http://i11.tietuku.com/6dc892cc5f456d1d.png)


### 上传本地博客到github（部署）
在`Git bash`中输入：
```
hexo d
```
进行上传（部署）操作。

首次使用git会询问github的账号信息：
```
Username for 'https://github.com' :
```
输入github上的用户名

```
Password for 'https://Jack0416@github.com':
```
输入github上的密码，输入时是没有*号提示的。

然后看到提示：
```
INFO  Deploy done: git
```
就表示上传到github成功。

浏览器中打开网址：
```
jack0416.github.io
```
其中`jack0416`换成自己的用户名，查看效果。


## 其它
**新建一篇博客文章**
依然如此，所有操作需要`Git bash`进入到博客目录进行操作，输入：
```
hexo n "Hello Hexo"
```
新建一篇以Hello Hexo为标题的文章。然后，资源管理器进入到博客目录下的`source/_posts`目录，可以看到有一个与标题名相同的md文件（Markdown文件），用记事本打开看到有以下默认内容：
```
---
title: Hello Hexo
date: 2016-02-18 13:13:38
tags:
---
```
两个`---`之间的是文章的信息，要写文章的内容，需要另起一行。文章支持Markdown写法（推荐），当然也支持html写法。

编辑好后，在`Git bash`中，输入
```
hexo g -d
```
本地产生博客页面，按照前面的方法输入账号信息上传到github。

**博客自定义**
博客要自定义，关键文件是`_config.yml`，可以根据自己需要进行修改，说明请看[Hexo官方文档](https://hexo.io/zh-cn/docs/configuration.html)。
如果不喜欢默认博客主题，也可以换。下载一个喜欢的主题到博客目录下的`themes`文件夹下，并修改`_config.yml`中的`theme`设定，即可切换主题（默认的主题是landscape）。

为了方便，还可以设置使用ssh key来连接github等，免去每次部署博客时要输入账号和密码的麻烦，可以自己查找SSH key相关资料，这里略~