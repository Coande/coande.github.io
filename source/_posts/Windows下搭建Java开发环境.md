title: Windows下搭建Java开发环境
tags:
  - Java
  - jdk
  - jre
id: 169
categories:
  - 技巧
date: 2015-03-10 12:00:26
---

虽然早已搭建过Java开发环境，但现在真正的在课堂上开始学Java了，看了下书，也悟到了一些新知识，所以顺便将它记录下来了。<!--more-->

首先，我们需要到Oracle官网下载一个JDK（Java Development Kit即Java开发工具集）。

然后，打开JDK安装包，下一步……这里需要提一下的是，自定义安装时我们可以不安装公共JRE（Java Runtime Environment），因为开发工具里面已经包含了一个专用的JRE（在jdk目录下）。两者主要差别：专用JRE比公用JRE多了个Sever的VM（Virtual Machine即虚拟机）执行选项。

安装完成后我们即可以在JDK的目录下的bin（binary即二进制文件）子目录下新建Java的源文件进行coding，coding完成后需要启动DOS进入到这个bin目录执行javac/java命令进行编译/运行。但是我们为了方便起见我们往往需要设置一下环境变量。

依次右键我的电脑-高级系统设置-环境变量，在系统变量下找到Path（路径）变量，点击编辑，变量值栏加上JDK下的bin子目录的路径，用英文半角输入分号来分隔已有的值。这个Path变量的作用是：我们不需要进入到bin就可以使用bin目录下的可执行文件（如javac.exe，java.exe）。也就是说我们不需要再在bin目录下新建java源文件，随便一个目录下新建源文件文件即可（但你还必须在DOS下进入到该目录进行编译/运行）。

设置了Path变量还不够，我们还得设置一下CLASSPATH变量。若没设置CLASSPATH（类路径），可能在执行某些复杂的Java的class时会报错（估计是这样的，没去试过）。我们需要在CLASSPATH变量值（没有这个变量的话就新建一个）中加上jdk目录下的lib（library即库文件）子目录下的dt.jar、tools.jar的路径和“.”（表示当前路径），不同路径之间也是使用半角英文分号隔开。这个环境变量的作用是：当运行（java \*\.class）class时找到class文件的，其中dt.jar和tools.jar的作用是其它什么辅助的吧（不太清楚）。当然你也可以固定一个文件夹用来coding，然后将这个文件夹的路径添加进CLASSPATH变量值中就不用进入到这个目录后再执行程序（java *\.class）。

<br />
**总结一下：**
Path变量：加入jdk下的bin目录路径，如：

	C:\Program Files\Java\jdk1.8.0_25\bin;
	
CLASSPATH变量：加入jdk目录下lib子目录下dt.jar，tools.jar的路径和“.”。如：

	.;C:\Program Files\Java\jdk1.8.0_25\lib\dt.jar;C:\Program Files\Java\jdk1.8.0_25\lib\tools.jar;

<br />
**Tips：**
win8就别设置JAVA_HOME变量来使用相对路径（变量值中含有%JAVA_HOME%）了，使用绝对路径就好了，有些win8的电脑使用相对路径可能会出现问题（环境变量设置好后时有效时无效，有效的时候重启后又无效了）。