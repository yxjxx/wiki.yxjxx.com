---
title: "vim base"
date: 2015-08-02 19:50
---

##1. 三种模式
1. 命令模式(normal/command mode)
2. 插入模式(insert mode)
3. EX模式(line mode)

###1. 在命令模式下

```
i : 光标前输入
I : **在光标所在行的行首插入**
a : 光标后输入
A : **在光标所在行的行尾插入**
o : 在当前行的下面新建一行
O : 在当前行之前插入新行
r : 仅仅替换当前字符
R : 替换当前字符并且自动调到下一字符
~ : Switch case
cw: 替换从光标到单词结束,并进入插入模式
x : 删除光标所在位置的字符(支持数字,如4x:删除光标加其后的字符一共4个)
dd: 删除整行
u : 撤销上一次操作
U : 撤销当前行的所有的修改
yy: 将当前行的内容放入缓冲区(复制当前行)
nyy : 将接下来的n行的内容放入缓冲区(复制n行)
p : 将就缓冲区的文本放入光标后(粘贴)
P : 在当前位置之前粘贴
/ : 向下查找关键字，n继续向下
? : 向上查找关键字，N继续向上

```

###2.插入模式

```
按i,I,a,A,o,O,r,R进入输入文本
```


operators and motions 模式

```
比如`d`是一种 operator 表示 delete , motion 就是光标的移动,常见的有
w:一个单词(光标当前位置到单词结尾包含空格)
e:当前单词的结尾,比w少一个空格
$:行尾
```

`c` 也是一种`operator`表示 change ,比如 `ce`:delete the word to the end and place you in the INSERT MODE,就是相当与`de+i`

###3. EX模式

```
在命令模式下输入':'进入EX模式

w : 保存
q : 退出
wq: 保存并退出
x : 保存并退出
q!: 不保存
:set nu : 显示行号
:! 系统命令 执行系统命令
:sh 切换命令行,按<ctrl>+d返回刚才的vim界面;
```

###4. 取消和恢复

```
命令模式下:
u: 取消上一次的改动   类似于<Ctrl>+z
<Ctrl>+r : 恢复  类似于<Ctrl>+y
```

###5. 同时编辑多个文件


```
加载/保存/推出/修改文件(缓存)
:e Edit the current file. This is useful to re-edit the current file, when it has been changed outside of Vim.
:e <文件路径>  : 打开该文件
:saveas <文件路径> : 保存到指定的文件,类似于另存为
:x,ZZ或者:wq : 保存和退出 (:x 如果可能的话，只保存)
:q! : 退出但不保存，使用:qa!，即使在缓存中还有已经修改的也会退出。
:bn(对比:bp) : 显示下一个(上一个)文件缓存
```

```
将选中的文本写入到新的文本文件中
VISUAL MODE  ---> `:w FIELNAME` (将视图模式选中的文本写入到FILENAME文件中)

将另一个文本中的内容插入到当前文本`:r FIELNAME`
也可以是输入输出流比如`:r !ls`

打开多个文件
vim filename1 filename2

```

```
分割窗口
:sp{filename}
<ctrl>+w+向上箭头
<ctrl>+w+向下箭头，切换工作区
ctrl+w连按两次在打开的多个文件之间切换
```


###6. 帮助查询

命令模式下

1. `:help`查看VIM帮助文件(完整版,英文)
2. `:help <cmd>` :查看某一命令的帮助
3. vimrc中的很多设置也可以通过`:help showcmd`这样的方式查看
4. 另外`/usr/share/vim/vim74/doc/options.txt & vimrc_example.txt
5. Tab键补全
6. Ctrl+D显示一个可供补全的列表
7. :help c_CTRL-D
8. :help vimrc-intro

帮助手册查看用到的快捷键:

```
跳转到一个主题: 将光标置于标签 (例如 usr_01.txt) 上然后输入 CTRL-]。
跳回: 键入 CTRL-T。
翻页：键入 CTRL-F/B

```
