---
title: "pipe"
date: 2015-07-27 18:58
---

pipe-base
======================

Linux管道重定向基础
2013/8/17

-------------------
管道及重定向就是Linux多命令协作的基础机制
管道通常用来组合不同命令
重定向通常用来保存输出信息

**Linux 的 Shell 对数据流进行以下分类定义：**

```
1. stdin     标准输入  编号为：0   默认：键盘
2. stdout   标准输出  编号为：1   默认：终端
3. stderr    标准错误  编号为：2   默认：终端
```

**重定向用来控制终端数据流：**

```
1. >       将标准输入以覆盖形式重定向到指定文件，如：ls > outfile
2. >>      将标准输入以追加形式重定向到指定文件，如：ls >> outfile
3. <       重定向标准输入   如：grep linuxcast < /etc/passwd
4. 2>      重定向标准错误
5. 2>&1    将标准错误合并到标准输出中
6. &>      将标准错误合并到标准输出中
```

黑洞设备 : `/dev/null`

**命令执行的判断依据**
命令回传码:若前一个命令执行的结果为正确,在Linux下面会回传到一个 `$?=0`的变量中

```
1. cmd1 && cmd2 如果1 stdout,会执行2
2. cmd1 && cmd2 如果1 stderr,不会执行2
3. cmd1 || cmd2 如果1 stdout,不会执行2
4. cmd1 || cmd2 如果1 stderr,会执行2
```

![Terminal](https://i.imgur.com/S1h8HH2.png)


**管道**

1. 管道命令仅会处理stdout不会去处理stderrout
2. 管道命令必须要能够接收来自前一个命令的数据成为stdin

```
管道“|”用以将一个命令的标准输出作为另一个命令的标准输入：

cmd1 | cmd2
```


