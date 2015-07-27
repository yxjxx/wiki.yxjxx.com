---
title: "zsh"
date: 2015-07-27 18:26
---

zsh configuration guide
================
<br/>

##参考资料:

1. [Mac技巧_终极shell](http://macshuo.com/?p=676)
2. [fooCoder_我在用的mac软件(2)-终端环境之zsh和z(*nix都适用)](http://foocoder.com/blog/wo-zai-yong-de-macruan-jian-2.html/)
3. [zsh – 给你的Mac不同体验的Terminal！](http://leeiio.me/bash-to-zsh-for-mac/)
4. [选择zsh的9个理由](http://lostjs.com/2012/09/27/zsh/ "")
4. [oh my zsh github mainpage](https://github.com/robbyrussell/oh-my-zsh)

**上面3篇博文的介绍大同小异,oh my zsh是简化zsh配置的一个开源项目**

-----------------------

###1. 查看自己的系统已经安装了哪些shell
    cat /etc/shells
我的Linux Mint15默认安装下面的shell

```
/bin/sh
/bin/dash
/bin/bash
/bin/rbash
```
-------------------
###2.安装zsh
Ubuntu系

    sudo apt-get install zsh

Redhat系

    sudo yum install zsh

安装完成之后再查看一下

```
/bin/sh
/bin/dash
/bin/bash
/bin/rbash
/bin/zsh
/usr/bin/zsh
```
现在就可以切换到zsh了

    #chsh -s /bin/zsh
    重启电脑之后生效，以后新开的Terminal就都是zsh了
--------------------
###3. 安装oh my zsh

    wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh

###4. 配置zsh

zsh的主要配置集中在~/.zshrc文件中
用vim打开，可以看到

```
# Path to your oh-my-zsh configuration.
ZSH=$HOME/.oh-my-zsh
......
# Customize to your needs...
export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
```
一大段配置zsh的示例,最后说你可以按照自己的需求自定义

#####环境变量
    export PATH=$PATH:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
    已经自动导入了bash的环境变量，还可以自己按要求添加

#####别名设置
```
alias cls='clear'
alias ll='ls -l'
alias la='ls -al'
alias -s md=mdcharm   #在命令行直接输入后缀为 md 的文件名，会在 mdcharm 中打开
alias -s c=vi         #在命令行直接输入后缀为 c 的文件名，会在 vi 中打开,下类似
alias -s gz='tar -xzvf'
alias -s tgz='tar -xzvf'
alias -s zip='unzip'
alias -s bz2='tar -xjvf'
```
#####主题设置
在~/zshrc文件中可以看到一行

    ZSH_THEME="robbyrussell"
    robbyrussell是默认主题
    在~/.oh-my-zsh/themes目录下还有几十种主题可以供你选择

按照Mac君的设置修改 robbyrussell.zsh-theme文件的第一行

```
PROMPT='%{$fg_bold[red]%}➜ %{$fg_bold[green]%}%p %{$fg[cyan]%}%d %{$fg_bold[blue]%}$(git_prompt_info)%{$fg_bold[blue]%} % %{$reset_color%}>'
```
c改为d（c为相对路径，单位绝对路径），在最后加上一个'>'符号

#####插件
在~/.zshrc文件中可以看到这么几行

```
# Which plugins would you like to load? (plugins can be found in ~/.oh-my-zsh/plugins/*)
# Custom plugins may be added to ~/.oh-my-zsh/custom/plugins/
# Example format: plugins=(rails git textmate ruby lighthouse)
plugins=(git)
```
oh my zsh为我们提供了大量好用的插件
使用的方法是在

    plugins=(git)中加入我们想用的的插件
    plugins=(git autojump github ruby python)
    使用方法查看插件目录下的*.plugin.zsh文件
#####git
默认启用了git插件：功能就是在每一个git管理的文件夹中显示git status,并且简化了大量的命令

```
随便拷贝一段看看,这些别名都可以在~/.oh-my-zsh/plugins/git/git.plugin.zsh文件中查看的到
# Aliases
alias g='git'
compdef g=git
alias gst='git status'
compdef _git gst=git-status
alias gd='git diff'
compdef _git gd=git-diff
alias gl='git pull'
compdef _git gl=git-pull
alias gup='git pull --rebase'
compdef _git gup=git-fetch
alias gp='git push'
compdef _git gp=git-push
alias gd='git diff'
.......
```
#####autojump
安装

    wget https://github.com/downloads/joelthelion/autojump/autojump_v21.1.2.tar.gz

解压缩后进入目录，执行

    ./install.sh

安装完成之后atuojump会返回告诉你
![autojump安装成功之后](http://ww4.sinaimg.cn/large/81d2b157jw1e7l5l9v896j20jt04igm7.jpg)
完成以上两步之后,就可以体验atuojump的强大了
```
    ..    #cd ..
    ~     #cd ~
    j auto #因为我们刚刚访问过autojump_v21.1.2目录所以 ‘#j auto’可以直接跳转到‘/home/yxj/autojump_v21.1.2’目录下
    等等超级多的强大功能，就等你自己去挖掘了
```



####5. 使用zsh（那些我觉得的好的功能）
0. 兼容bash,无痛转移
1. 超级强大的<Tab>补全,连按两下<Tab>会列出所有供选择的项,按<tab>方向键可以切换,
    也支持<Ctrl>+npfb(VIM)
    <Ctrl>+n 向下
    <Ctrl>+p 向上
    <Ctrl>+f 向下翻页
    <Ctrl>+b 向上翻页

    ![zsh补全.png](http://ww3.sinaimg.cn/large/81d2b157jw1e7ry1p92m4j20ej057mxy.jpg)

2. zsh 除了支持目录的补全，还支持命令选项的补全，例如 ls -<TAB><TAB> 会直接列出所有 ls 的参数，
   再也不会出现一个命令打到一半，忘记参数导致重开一个 terminal man 一把。
   ![zsh命令参数补全](http://ww2.sinaimg.cn/large/81d2b157jw1e7ryfepje2j20hj09uaco.jpg)
3. kill 进程名<Tab>  会直接转换成id
   ssh
   apt-get
   等等,各种补全
4. 更智能的目录补全
   cd /h/y/D/L/c/<Tab>会自动补全成
   cd /home/yxj/Dropbox/Linux/configuration(当然前提是这种匹配是唯一的)
   ![zsh<Tab>首字母匹配](http://ww4.sinaimg.cn/large/81d2b157jw1e7ryuksq5cj20dw02w3yv.jpg "")

5. 记录你切换过的路径直接输入1~9切换(0是当前目录),用d查看当前stack中存放的历史目录

    ![1~9切换目录](http://ww2.sinaimg.cn/large/81d2b157jw1e7rz40abb3j209e075jrv.jpg)
6. 更强大的目录跳转可以用autojump插件,autojump插件可以记住你所有访问过的目录
   直接`#j Dr`就能跳转到Dropbox目录

   ![atuojump](http://ww2.sinaimg.cn/large/81d2b157jw1e7rzbbzfmmj209d03dmx8.jpg "")

7. 更强大的alias

```
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"
#####别名设置
alias -s md=mdcharm   #在命令行直接输入后缀为 md 的文件名，会在 mdcharm 中打开
########
```
8. 丰富漂亮的主题

```
# Set name of the theme to load.
# Look in ~/.oh-my-zsh/themes/
# Optionally, if you set this to "random", it'll load a random theme each
# time that oh-my-zsh is loaded.
ZSH_THEME="robbyrussell"
```
还可以自己改主题

9. 插件体系
    git,github等等很实用

##说明

原文写作于2013年7月，2015年7月整理发布在我的个人 Wiki 上。

1. oh-my-zsh 自带的插件`z`实现了和`autojump`同样的功能，开启方法更简单。
2. 插件`sudo` 只要按`Esc`两下就可以在输入命令的时候在前面加上 sudo
3. web-search `google keyword` in your terminal.




