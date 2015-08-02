---
title: "vimrc"
date: 2015-08-02 20:40
---

##vim配置文件

整体的vim设置文件在 `/etc/vim/vimrc` (有的发行版本在 `etc/vimrc`)
但是最好在`~/.vimrc`中增加你自己的配置（第一次使用要新建该文件）
gvim和vim是共用`~/.vimrc`文件的，gvim还会额外的加载`.gvimrc`文件

```
比如：（可以用英文的双引号注释）
set nu      "显示行号
syntax on   "语法高亮
```

效果:

![vim配置之后的效果](http://ww4.sinaimg.cn/large/81d2b157jw1e7mh7mtanuj20i905ut94.jpg)

vim的配置是一个大工程,我在Github维护着我的 [.vimrc](https://github.com/yxjxx/dotfiles) 文件和 `.gvimrc` 文件,这里就不详细写了。

另外:
.vim是Vim的主配置文件夹，位于当前用户的主目录下(Windows下在C:\Program Files (x86)\Vim\vim74)，可以用cd ~/.vim进入。该文件夹一般用来放置插件和相关的帮助文档，常用的目录结构包括：
![.vim](http://ww4.sinaimg.cn/large/81d2b157jw1e81uqe1x42j20cn081js9.jpg "")

-------------------
