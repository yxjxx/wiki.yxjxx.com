---
title: "substitute"
date: 2015-08-02 20:38
---

```
old是需要替换的字符串,new是替换后的字符串

:s/old/new <ENTER>替换当前行的第一个old

:s/old/new/g当前行的所有old进行替换,

如果需要进行全局替换,则要:
:%s/old/new/g
如果需要对指定部分进行替换,可以用V进入visual模式,再进行
:s/old/new/g
或者可以指定行数对指定范围进行替换:
:100, 102s/old/new/g(100-102行)
```

