---
title: "git"
date: 2015-07-27 18:40
---

Git 和 Github的使用说起来不算难,对着官方指南看一遍基本就能开始用了,高级特性暂且先不研究,需要的时候再学.


但是经过一段时间的与git和github打交道,发现至今没有领略的git的精髓部分,每次就一个分支,每次就修改提交再修改再提交,没有多分支,没有版本回溯没有文件差异对比.感觉和以前手动控制版本没有太大的差别


--------------------------

###1.安装配置git
*`#sudo apt-get install git`*
**配置用户名和邮箱**
>`$git config --global user.name "yourname"`
>`$git config --global user.email "youremail@gmail.com"`

**配置git commit时的文本编辑器**
>`$git config --global core.editor "vim"`

**设置Github密码缓存**
>`$git config --global credential.helper 'cache --timeout=3600'`

以上为全局设置会保存到~/.gitconfig文件中格式如下
```
[user]
    name = yourname
    email = youremail@gmail.com
[core]
    editor = vim
[credential]
    helper = cache --timeout=3600
```


-----------------------
###2.连接Github
**Linux下生成ssh连接的密钥对(在Windows下github客户端会帮你自动完成这些工作)**
官网教程： [generating-ssh-keys](https://help.github.com/articles/generating-ssh-keys)

1.生成密钥对，这样项目可以push到GitHub上, 生成密钥对时不输入密码,省得以后每次push都要输密码.
```
#ssh-keygen -t rsa -C "xxx@gmail.com"
```
2.将.ssh/id_rsa.pub拷贝到GitHub网站 [Add SSH Key](https://github.com/settings/ssh)

3.测试是否配置成功：
```
#ssh -T git@github.com
```

---------------------------------
###3.建一个Github仓库
1.先在网页端新建一个仓库（可以不为空）
2. `git clone git@github.com:youname/Test.git`
3.不用 `git init` 直接增加或者修改文件
4.git remote -v 可以查看到origin已经连上github了
5.下次直接git push -u origin master

------------------------
或者（我本地有一个仓库，现在要连接远程仓库）
1.先在网页端新建一个空的仓库，记下它的连接如： git@github.com:yourname/Test.git

在本地文件夹

```
git init
git add [filename] or git add ./*  全部加到缓冲区
git commit  不带参数，打开vim编辑，一个好的习惯是第一行简要描述，下面一段话详细描述
上面的两步可以合做一步
```

2.把本地仓库push过去

```
git remote add origin git@github.com:yourname/Test.git
git push -u origin master
```

-------------
###4.撤销操作
    修改上一次提交：
    git commit --amend

    取消已经暂存的文件
    运行git status即可看到
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)

    取消对文件的修改：
    use "git checkout -- <file>..." to discard changes in working directory
    这条命令有些危险，所有对文件的修改都没有了，因为我们刚刚把之前版本的文件复制过来重写了此文件

---------------
###5. 远程仓库的使用
    git remote      //查看当前配置有哪些远程仓库
    git remote -v   //显示详细信息包括 对应的克隆地址
    git remote add [shortname] [url]  //添加一个新的远程仓库
    git fetch [remote-name]     //从远程仓库抓取数据到本地
    fetch 命令只是将远端的数据拉到本地仓库，并不自动合并到当前工作分支，只有当你确实准备好了，才能手工合并。
    git pull       //要从原始克隆的远端仓库中抓取数据后，合并到工作目录中的当前分支
    git push [remote-name] [branch-name]        //将本地仓库中的数据推送到远程仓库
    git remote show [remote-name]       //查看某个远程仓库的详细信息
    git remote rename       //修改某个远程仓库在本地的简称
    git remote rm  [remote-name]         //移除远端仓库


------------------------------------------
###6. Git分支(branch)

[Git pro相关章节](http://git-scm.com/book/zh/Git-%E5%88%86%E6%94%AF "")

```
git branch testing 新建分支
git checkout testing 切换到testing分支

切换分支的时候最好保持一个清洁的工作区域,留心你的暂存区或者工作目录里，那些还没有提交的修改，它会和你即将检出的分支产生冲突从而阻止 Git 为你切换分支

git checkout -b issue53   新建名为issue53的分支,并切换到issue53分支

git branch -d testing 删除testing分支
git branch 查看当前有哪些分支,以及当前正处于哪一个分支
git merge testing(branchname)  合并testing分支到当前分支



```

-----------------------------------
###7. Git tag




----------------------

1. git不跟踪空的文件夹
2. git push origin master -f 强制更新远端仓库和本地一样,常见与本地有版本回溯,git push报错, 而你有非常确认本地修改是完全正确的情况下.
3. git rm --cached FILENAME  删除不再跟踪的文件
4. git 开dev分支,一直push,master只merge主要版本
5. git-flow

###说明

原文写作于2013年7月，2015年7月整理发布在我的个人 Wiki 上。

1. 在 SourceTree 是很好用的 git 图形客户端。
2. coding 的速度超级快。
3. 关于 git 的使用教程一本 git pro 就够了，其它主要靠实操。
