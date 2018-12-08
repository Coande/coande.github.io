title: 解决Hexo导入Wordpress的文章后文件名问题
date: 2015-08-01 22:30:48
tags:
 - Linux
 - shell
 - hexo
categories:
 - 技巧
---
将博客文章从wordpress转移到hexo过程中遇到了个小问题。从wordpress导出的文章，导入到hexo后，发现`source/_post/`下多了一堆十六进制混杂着英文作为文件名的`.md`文件。其实，注意观察我们也可以知道，wordpress导入文章到hexo实际上是将一个`xml`文件中的各文章转换成`source/_post/`目录下的`Markdown`格式的`md`文件，而这些文件名的命名则是根据文章的`title`命名的，而十六进制的出现是因为文章标题中的中文所致。在wordpress转移到hexo的过程中，我们的文章难免会出现些问题，我们可能还需要对导入的文章修改一下。但是这十六进制的文件名不利于我们辨认哪个文件是我们的需要修改的文件。其实，我们完全可以根据自己的需要打开文件，查看文件中的`title`进行手工重命名文件。但有个问题，如果我的文章都是中文标题，而且文章数量庞大，一大堆以十六进制作为文件名的文件啊。前段时间学了Linux的`shell`编程，这下子用的上了，写了如下脚本：<!--more-->
```
#!/bin/bash
#Author: Coande  Email: e12e@qq.com
#rename the md file of hexo

#将当前目录下的文件列表保存到“filename.list”文件中
ls > filename.list
#依次读取“filename.list”中的文件名
for filename in $(cat filename.list)
	do
		#判断当前读取到的文件名是否本脚本和本脚本生成的文件，不是才执行
		if [ "$filename" != "rename.sh" -a "$filename" != "filename.list" ]
			then
				#获得<filename>对应文件中的title的值，并对title值中的空格、“/”、“!”做了处理
				title=$(cat $filename | grep title | sed -n '1p' | cut -d ":" -f 2 |  sed -e 's/ /_/g ; s/^_//g ; s/\//-/g ; s/\!/\\!/g')
				#过滤掉文件内容中没有title的文件和文件名正常的文件
				if [ -n "$title" -a "$filename" != "$title.md" ]
					then
					#将<filename>文件名重命名为title的值.md
					mv $filename $title.md
				fi
		fi
	done
rm -f filename.list
echo done!
```
<br />
运行脚本前：
![运行脚本前图片](http://i3.tietuku.com/1d9003e048e3e674.jpg)


运行脚本后：
![运行脚本后图片](http://i3.tietuku.com/9171637475818a99.jpg)
<br />

这是我的第一个自己想自己写的shell脚本，写完运行成功解决了自己的问题，想想都有点小激动^_^，感觉Linux太强大了。第一次写哈，难免会有想得不周全的地方，有问题欢迎指出。
<br />

**Tips**：将上面代码复制到hexo博客的`source/_post`下`新建`的一个以`rename.sh`作为文件名的文件中，命令行中执行`bash ./rename.sh` 运行脚本即可。运行后提示`done!`即表示成功执行了。Windows中也可以直接双击该文件来执行。

***
2015/8/4更新：犯傻了，前面忘记了ls可以用通配符将`.md`文件单独筛选出来了，本来很简单的想得复杂了。这样又可以省去一个判断，快了点……
```
#!/bin/bash
#Author: Coande  Email: e12e@qq.com
ls *.md > filename.list
for filename in $(cat filename.list)
	do
		title=$(cat $filename | grep title | sed -n '1p' | cut -d ":" -f 2 |  sed -e 's/ /_/g ; s/^_//g ; s/\//-/g ; s/\!/\\!/g')
		if [ -n "$title" -a "$filename" != "$title.md" ]
			then
				mv $filename $title.md
		fi
	done
rm -f filename.list
echo done!
```