---
title: "bash base"
date: 2015-07-28 16:09
---

bash-base
===========
**一些基础常识**

查看本机已经安装了的shell:

    #cat /etc/shells

![我的shells](http://ww1.sinaimg.cn/large/81d2b157jw1e7nkaq6hw7j209a03rjri.jpg)

查看正在使用的shell:

    #echo $SHELL

![我的正在使用的shell](http://ww2.sinaimg.cn/large/81d2b157jw1e7nkcnvq1rj205r00x744.jpg)

切换shell:

    #chsh -s /bin/zsh

![切换到zsh](http://ww4.sinaimg.cn/large/81d2b157jw1e7nklb64xpj20cz08amxz.jpg)

重启系统之后生效

查看/etc/passwd文件了解更详细的关于每个用户的默认shell的信息:

![shell详细信息](http://ww4.sinaimg.cn/large/81d2b157jw1e7nkqek1q3j20i70hpaeu.jpg)


shell的命令历史记录功能:

    bash存放在~/.bash_history
    zsh存放在~/.zsh_history
    在终端中输入命令时先按下<Ctrl>+r之后shell就会去历史记录里面搜索是否有匹配的,肯定是时间倒序匹配啦!
    就是说有多条记录匹配的情况先显示的时间最近的一条命令


命令与文件补全`<Tab>`键,就不细说了,都知道`<Tab>`的好,特别是在zsh下

命令别名设置(alias)

    alias命令显示你现在已经设置的别名
    alias lm='ls -al'  #可以设置别名

![alias](http://ww2.sinaimg.cn/large/81d2b157jw1e7nljoxl32j20b104mdg9.jpg)

通配符(正则表达式)

```
*表示一个或多个字符
?表示一个字符
[abc]表示a或者b或者c
等等
```

查询是否为bash shell的内置命令  type

```
type [-afptP] 名称 [名称 ...]

```

命令太长,转义字符

    命令太长,一行打不下，先输入一个'\'再输入一个<Enter>
    换行之后可以看到一个'>'符号,就是转义成功了

![转义](http://ww1.sinaimg.cn/large/81d2b157jw1e7nmjx2mdzj20h801rq30.jpg)


环境变量都全部大写

例如:PATH HOME MAIL SHELL

显示变量的内容;echo命令

    echo $PATH
    echo ${PATH}
    两种方式都可以

设置自己的shell变量:

    未设置的变量默认为空
    设置变量myname : 直接输入  myname=yxjxx
    取消变量myname : unset myname

![设置变量](http://ww4.sinaimg.cn/large/81d2b157jw1e7nnfvhl2vj209q05n3yy.jpg)

双引号单引号内的变量:

    双引号内的特殊字符,可以表示它的指代义
    单引号内的特殊字符,就只能是字符了
    双引号内的特殊字符如果不想要它的指代义可以用'\'转义掉

![引号内的变量](http://ww2.sinaimg.cn/large/81d2b157jw1e7nnrv5rw5j20940ad3zi.jpg)


在一串命令中用到其它命令的输出信息时:

    version=$(uname -r)
    version=`uname -r`

![](http://ww1.sinaimg.cn/large/81d2b157jw1e7nnwfkv3bj209t05x74w.jpg)


为变量增加字符:

    PATH=$PATH:/home/bin
    PATH="$PATH":/home/bin   或者
    PATH=${PATH}:/home/bin
    PATH="${PATH}":/home/bin 都行

![](http://ww2.sinaimg.cn/large/81d2b157jw1e7no1wpg10j20i7065400.jpg)


若该变量需要在其它子进程中执行,则需要以export来使变量变成环境变量

    export var

一个习惯:通常系统默认变量为大写,用户自定义的变量最好设为小写



查看环境变量

    env
    set
    export


子进程仅会继承父进程的环境变量,不会继承父进程的自定义变量
将环境变量转换成自定义变量用 `declare`命令


------------------
变量的键盘读取,数组与声明

    read [-pt] variable
    -p : 后面接提示语
    -t : 后面接等待的秒数


```
declare [-aixr] variable

-a : 数组
-i : 整数
-x : 将后面的variable变成环境变量同export
-r : 设置成readonly
```

`文件系统及程序的限制关系:ulimit`


变量的测试与内容替换:

    var=${str-expr}
    等等...


--------------
查找命令的顺序:

1. 以绝对或相对路径执行的命令,已经指定了文件
2. 由alias找到该命令执行
3. 由bash内置的命令来执行
4. 通过${PATH}变量找到第一个命令来执行
5. 可以通过`type -a cmd`(cmd为你要查询的命令)查看找寻顺序


-------------------

loginshell和non-loginshell读取的配置文件不一样


loginshell会在bash登录的时候去读取

    /etc/profile(系统整体的设置,不要去修改)
    ~/.bash_profile
    或~/.bash_login
    或~/.profile


--------------
终端机的环境设置

    stty(自己man一下吧)
