---
title: "regular expression"
date: 2015-07-28 16:18
---

regular-expression
========================

参考资料:

1. [MSDN中关于正则的文档](http://msdn.microsoft.com/zh-cn/library/vstudio/az24scfc.aspx)
2. [正则30分钟入门](http://see.xidian.edu.cn/cpp/u/zhengze/)
3. [查表--所有元字符](http://see.xidian.edu.cn/cpp/html/1427.html)

------------------------------------

**写在前面,很多初学者都会遇到的一个疑问----正则与通配符不一样:**

正则表达式的特殊字符与一般在命令行输入命令的"通配符"并不相同,例如在通配符中`*`代表的是0到无限多个字符的意思,但在正则表达式中,`*`则是重复0到无穷多个得到前一个字符的含义,使用的意思并不相同,不能搞混了!

例如:删除时使用的`rm *.txt` 中的`*`指的是是通配符，意为匹配0个字符或多个字符，正则中的`*`是匹配该字符的前一个字符的0次或多次出现。就是说在正则中使用`*`，`*`的前面必须要有字符。

再例如通配符 zh*.txt 会匹配 zhh.txt、zhxx.txt、zhzh.txt……
而正则表达式中的 zh*.txt 会匹配 zh.txt、zhh.txt、zhhh.txt……

一个例子
```
原来bash用的是通配符,zsh用的标准正则,把要匹配的字符串打上引号是一个好习惯
zsh中的
$sudo apt-get remove --purge 'printer-driver.*'
这样就和bash里面的
$sudo apt-get remove --purge printer-driver*
效果一样了
```

---------------------
**正则表达式基础**

1. `^word` : 查找的word字符在行首,即以word开头的行
    `grep -n '^#' regular-expression` : 在文件`regular-expression`查找以`#`开头的行

2. `word$` : 查找以word结尾的行
    `grep -n '#$' regular-expression`

3. `.` : 代表一定有一个字符,除换行符以外的任意一个字符;`\S`与之类似表示 不是空白字符的任意字符(`.`可以匹配空格,在例子2中会涉及到)
4. `*` : 重复0个到无穷多个前一个字符
5. [acfg] : 匹配a,c,f,g中的任一个
6. `[0-9]or[a-z]or[0-9a-zA-Z]` : 匹配其中的一个字符,`\d`:表示一个数字
7. `[^list]` : 取反,匹配不在list中的项
8. `\{n,m\}` : '\'是转义字符,连续n到m个前一个字符     `\{n\}`:表示连续n个前一个字符     `\{n,\}` : 连续n个以上
9. `\b` : 表示单词的开头或结尾.`\bhi\b`只能匹配单词`hi`而不能匹配`his`或`shi`等字符串中的部分,而`\bhi`了一匹配`his`中的`hi`
10. `\w` : 匹配字母或数字或下划线,`\W`: 匹配任意不是字母，数字，下划线
11. `\s` : 匹配任意的空白符,`\S`:不是空白字符的任意字符
12. `\d` : 匹配数字等价于`[0-9]`,`\D` : 匹配任意非数字的字符




-----------------------
**扩展正则表达式**

1. `+` : 重复一个或一个以上的前一个字符
2. `?` : 0个或一个前一个字符 ,前一个字符可有可无
3. `|` : 用或的方式找出整个字符串
4. `( )` : 找出组的字符串   `'g(la|oo)d'` : 匹配glad和good
5. `( )+` : 多个重复组的判别  `echo 'AxyzxyzxyzC' | egrep 'A(xyz)+C'` : 匹配A开头C结尾中间有一个以上的'xyz'


-------------
**例子1**
Hi, I am Shirley Hilton. I am his wife.

用`I.*e`去匹配得到的是`['I am Shirley Hilton. I am his wife']`,称为贪婪匹配,`*`会匹配尽量长的结果

用`I.*?e`去匹配得到的是`['I am Shirle', 'I am his wife']`,称为懒惰匹配,最短匹配,在最后的图片爬虫中要用到

---------------
**例子2**
从下面一段文本中，匹配出所有s开头，e结尾的单词。

site sea sue sweet see case sse ssee loses

第一次我用的是`r"\bs.*?e\b"`结果为`['site', 'sea sue', 'sweet see', 'sse', 'ssee']
`出现了`sea sue`不满足单词的要求,就是说不能有空格,那么把`.`改为`\S`即可
`r"\bs\S*?e\b"`结果为;
`['site', 'sue', 'see', 'sse', 'ssee']`

----------
**例子3**
找出11位手机号码


`1\d{10}`

----------

**python中的正则**

直接逐行解释

```python
import re
text  = "123 123x 234x"
m = re.findall(r"1\d*[x]?",text)
if m:
    print m
else:
    print "not match"
```
结果:

```python
['123', '123x']
```

---------------------------

编译过后的正则,效率更高.

```python
import re
text  = "123 123x 234x"
r1 = r"1\d*[x]?"
obj_r1 = re.compile(r1)
# print type(obj_r1)
m = obj_r1.findall(text)
if m:
    print m
else:
    print "not match"
```

而且编译的过程中可以加入一些其它编译参数如`re.I`等

```python
import re
ignorecase_re = re.compile(r"yxjxx",re.I)#参数re.I表示忽略大小写
m = ignorecase_re.findall('yxjxx YXJXX yxjXX YxjXX')
if m:
    print m

else:
    print "mot match"
```
结果:

```python
['yxjxx', 'YXJXX', 'yxjXX', 'YxjXX']
```

--------------

更多的编译标志-flags

```
re.S  : 使 . 匹配换行在内的所有字符
re.I  : 使匹配对大小写不敏感
re.L  : 做本地化识别,匹配其它语言中的特殊字符
re.M  : 多行匹配,影响^和$
re.X  : 正则的多行
```

**一个补充知识**
在交互模式中可以看到以`'''`包含的字符串实际的存储是加上了`\n`的单行存储

```python
>>> s = '''
... Hello
... world
... I
... am
... yxjxx
... '''
>>> s
'\nHello\nworld\nI\nam\nyxjxx\n'
```

编译标志-flags的例子

```python
import re

#########  re.S
r1 = r'yxjxx.me'
print re.findall(r1,'yxjxxzme')
print re.findall(r1,'yxjxx\nme')
print re.findall(r1,'yxjxx\nme',re.S)
print re.findall(r1,'yxjxx\tme',re.S)

#########  re.M
s2 = '''
hello yxjxx
yxjxx hello
Hello yxjxx
'''
r2 = r"^yxj"
print re.findall(r2,s2)
print re.findall(r2,s2,re.M)

########### re.X
r3 = r"""
\d{3,4}
-?
\d{8}
"""
print re.findall(r3,'010-12345678')
print re.findall(r3,'010-12345678',re.X)

######### re.I
r4 = r"yx.xx"
print re.findall(r4,'yxjxx')
print re.findall(r4,'YXJXX')
print re.findall(r4,'YXJXX',re.I)
```

结果:

```python
['yxjxxzme']
[]
['yxjxx\nme']
['yxjxx\tme']
[]
['yxj']
[]
['010-12345678']
['yxjxx']
[]
['YXJXX']
```

------------

re库中常用的方法/属性

```
match()   开头有,返回一个match对象,开头没有返回空
search()  开头,中间,结尾有都行,返回一个对象
findall() 匹配所有,返回一个list
finditer() 与findall()类似,只是返回值为迭代器
```

match对象的方法

```
group()
start()
end()
span()
```

------------------
`re.sub`支持正则的替换
类似的
re.subn()
re.spilt()

```python
# -*- coding: utf-8 -*-
import re
s = "Hello yxjxx"
s1 = s.replace('yxjxx','python')
print s
print s1

s2 = s.replace('y...x','python')#字符串的replace方法是不支持正则的
print s
print s2


rs = r'y...x'
print re.sub(rs,'python','yxjxx yzzzx yzxzx yzzzz')
print re.subn(rs,'python','yxjxx yzzzx yzxzx yzzzz')

str = '123+456*78-9'
print re.split(r'\D',str)
```
结果:

```python
Hello yxjxx
Hello python
Hello yxjxx
Hello yxjxx
python python python yzzzz
('python python python yzzzz', 3)
['123', '456', '78', '9']
```

更多`re`模块的方法可以通过`dir(re)`和`help(re)`查看,当然你需要先`import re`


------------------------------
**python正则分组**

```python
import re

s = '''
find mp3 Hello src=twitter at today
you are Hello src=facebook at yesterday
I am yxjxx Hello src=youtube at tomorrom
'''
#找出Hello src=... at 式样的字符串
r1 = r'Hello src=.+ at'
print re.findall(r1,s)

#有的时候我们可能只需要src=后面的内容
#增加分组之后就会只返回分组里面的内容的匹配值
r2 = r'Hello src=(.+) at'
print re.findall(r2,s)
```

结果:

```
['Hello src=twitter at', 'Hello src=facebook at', 'Hello src=youtube at']
['twitter', 'facebook', 'youtube']
```


---------------
**一个小的实例--图片爬虫**

![src='](http://ww3.sinaimg.cn/large/81d2b157jw1e8zqii1tvcj20rr07jaef.jpg)

就如上图所示,一般网站上的图片链接都有一定规律,我们先取得网站的源代码,然后通过正则表达式匹配图片链接然后通过`urllib.urlretrieve()`下载下来即可

```python
import re
import urllib

def getHtml(url):
    page = urllib.urlopen(url)
    html = page.read()
    return html

def getImg(html):
    reg = r'src="(.*?\.gif)"'
    img_re = re.compile(reg)
    imglist = re.findall(img_re,html)
    x = 0
    for imgurl in imglist:
        urllib.urlretrieve(imgurl,'%s.gif' % x)
        x+=1
    return imglist

html = getHtml('http://photo.yxjxx.me/post/zhu-yin-gif')
print getImg(html)
print 'done'

```
