---
title: Node.js 项目打包成 exe 并注册成 Windows 服务
date: 2019-04-08 21:06:51
tags:
---

直接上 Demo: https://github.com/Coande/nodejs-pkg-nsis-demo


<!-- more -->

- 为什么需要注册成服务？为了不显示命令行窗口且开机自启动。
- 为什么需要把js项目打包成exe程序？自带Node.js运行环境，不需要再额外配置运行环境。
- 为什么要把程序打包成安装包？为了方便把程序注册成服务，简化操作。
- [node-windows](https://www.npmjs.com/package/node-windows) 也可以注册服务，但是不稳定。遇到过运行后服务注册不成功，也没有任何错误输出的情况。
- 利用 [pkg](https://www.npmjs.com/package/pkg) 可以把js项目打包成自带 Node.js 运行环境的exe程序。
- 利用 [NSIS](https://nsis.sourceforge.io/Main_Page) 可以把软件打包成安装包，可以自定义安装时的一系列动作。
- 添加服务，可以使用`Simple Service Plugin`，参看：https://nsis.sourceforge.io/NSIS_Simple_Service_Plugin
- 直接把普通程序注册成服务，是不能运行的：
![服务无法运行](https://i.loli.net/2019/04/10/5cadad290bc41.png)
> 可以用`srvany.exe`来帮助我们的程序以服务方式运行。可以参考：https://www.cnblogs.com/codealone/p/3156943.html

- 遇到中文（注释也不例外）时可能会报`Bad text encoding`相关的错误，可以在运行`makensis.exe`编译脚本时使用`/INPUTCHARSET UTF8`参数。参考：https://github.com/evshiron/nwjs-builder-phoenix/issues/17
- `pop $0`的含义：从栈中弹出变量并赋值给变量`$0`。其中，`$0`是内置变量，无需声明（非内置变量必须先声明），可以直接使用。栈和变量都是存储数据的方式，函数传参和返回值通常使用栈来传递。
- `+2`意思是跳到后面第二行代码执行。