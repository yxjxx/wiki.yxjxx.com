---
title: "tar"
date: 2015-07-28 14:13
---

Compressing files under Linux
============

***************
NO DEEP SHIT!

**************

本文简短的介绍一下三个命令,足够应对日常压缩,解压缩的任务.更复杂的命令参数可以自己`man`一下或者在网络上搜索.

`tar` : 打包命令,把一组文件和文件夹变成一个常规文件,没有压缩空间的功能.
`gzip` & `bzip2` : 具有压缩解压缩的功能,会将文件内容重新编码,节省空间.

-------------------------------

压缩文件
------

`tar -zcvf filename.tar.gz folder/file`

```
➜  /home/yxj/test  >ls
haha.txt  yxj.txt
➜  /home/yxj/test  >tar -zvcf mycompress.tar.gz
tar: Cowardly refusing to create an empty archive
Try `tar --help' or `tar --usage' for more information.
➜  /home/yxj/test  >tar -zvcf mycompress.tar.gz ./haha.txt ./yxj.txt
./haha.txt
./yxj.txt
➜  /home/yxj/test  >ls
haha.txt  mycompress.tar.gz  yxj.txt
```

1. `-z` : 使用gzip进行压缩
2. `-j` : 使用bzip2进行压缩,具有更高的压缩比 `tar -jcv -f filename.tar.gz folder/file`
2. `-c` : 表示压缩
3. `-v` : 显示详细信息
4. `-f` : 文件和文件夹列表
5. `filename.tar.gz` : 压缩之后的压缩包的名字
6. `folder/file` : 文件和文件夹列表,多个文件以空格隔开

注意到`-f`参数的含义,最好将`tar -zcvf filename.tar.gz folder/file`改写成 `tar -zcv -f filename.tar.gz folder/file`


*********************

解压缩
-----------------

将`-c`参数换成`-x`即可

`tar -jxv -f mycom.tar.bz2 ` : 将`mycom.tar.bz2`在当前目录下解压缩.

如果需要解压到制定的目录可以使用`-C`参数
`tar -jxv -f mycom.tar.bz2 -C ./folder/`

```
➜  /home/yxj/test/folder  >la
total 0
➜  /home/yxj/test/folder  >tar -jxv -f ../mycom.tar.bz2 -C ~/test/folder
./
./mycompress.tar.gz
./yxj.txt
./mycom.tar.gz
./haha.txt
➜  /home/yxj/test/folder  >ls
haha.txt  mycompress.tar.gz  mycom.tar.gz  yxj.txt
➜  /home/yxj/test/folder  >
```

只查看tar文件中包含那些文件不解压`-t`参数

```
➜  /home/yxj/test  >tar -jtv -f mycom.tar.bz2
drwxr-xr-x yxj/yxj           0 2014-03-12 09:12 ./
-rw-r--r-- yxj/yxj         291 2014-03-12 09:07 ./mycompress.tar.gz
-rw-r--r-- yxj/yxj         199 2014-03-09 19:13 ./yxj.txt
-rw-r--r-- yxj/yxj         677 2014-03-12 09:12 ./mycom.tar.gz
-rw-r--r-- yxj/yxj           0 2014-03-12 09:04 ./haha.txt
```

**********************

如果你使用强大的zsh可以按如下方式设置你的`.zshrc`,直接键入文件名,自动判断之后在当前文件夹解压,省去键入命令的麻烦

```

alias -s c=vim         #在命令行直接输入后缀为 c 的文件名，会在 vi 中打开,下类似
alias -s gz='tar -xzvf'  #在命令行直接输入后缀为 gz 的文件名，会用tar -xzvf解压
alias -s tgz='tar -xzvf'
alias -s zip='unzip'
alias -s bz2='tar -xjvf'
```


--------------------
