---
title: "markdown"
date: 2015-07-27 18:01
---

##参考资料列表：

1. [简明手册](http://ghosertblog.github.io/mdeditor/)  __同时可以作为在线编辑器__
2. [官方说明的简体中文翻译版](http://wowubuntu.com/markdown/)
3. [GitHub Flavored Markdown](https://help.github.com/articles/github-flavored-markdown)  **github增强版的Markdown**


-------------------------
##在用的编辑器

1. **windows** : [MarkdownPad](http://markdownpad.com/)(免费版不支持代码块，收费版没用过)
2. **Linux** : ReText `#sudo apt-get install retext`
3. **Win&Linux** [mdcharm](http://www.mdcharm.com/download.html) （win下的版本2013年4月开始收费,显示效果最接近github）
4. **Mac** : [Mou](http://mouapp.com/) （国产精品，Mac下最好的Markdown编辑器）
5. **Online** : [Dillinger](http://dillinger.io/#)  （多种主题切换，蛮漂亮的）

-----------------------------
##笔记

####1. 斜体和粗体

    *斜体*
    _斜体_
    **粗体**
    __粗体__

#####效果:
*斜体*
_斜体_
**粗体**
__粗体__

-------------------

####2. 多级标题
    表示一级标题
    =======
    表示二级标题
    -----
    #一级标题
    ##二级标题
    ###三级标题
    ######最多六级标题
#####效果:
表示一级标题
======
表示二级标题
------
#一级标题
##二级标题
###三级标题
######最多六级标题

-------------------

####3. 文字增加外链(注意一定要用英文括号)
    [github](https://www.github.com)
    <yourname@gmail.com>    //强制用链接表示，由于GFM会自动识别链接所以不要在github中不要'<>'也行
    <yxjxx.com>
#####效果
[github](https://www.github.com)

<yourname@gmail.com>    //强制用链接表示

<http://yxjxx.com>

--------------------------
####4. 图片外链
    ![图片说明](图片网址)
#####效果:
   ![ 小铃木爱理](http://ww2.sinaimg.cn/small/81d2b157jw1e7jaf55ttuj20rs15o0yd.jpg)
<!--![铃木爱理](http://ww2.sinaimg.cn/mw690/81d2b157jw1e7jaf55ttuj20rs15o0yd.jpg)-->

--------------------------------
####5. 换行
    行末增加两个空格表示换行
    <br/>也能表示换行
#####效果:

你好<br/>
世界

--------------------------------
####6. *,- ,+都能表示无序列表
    + 首先
    + 其次
    + 然后
    + 最后
    * 可以
    * 混排
#####效果:
+首先
+其次
+然后
+最后
-可以
*混排
#####(为什么不行?)
#####因为缺少了一个空格
+ 首先
+ 其次
+ 然后
+ 最后
- 可以
* 混排

-------------------
####7. 数字加点表示有序列表
    1. 第一(和无序一样要有一个空格)
    2. 第二
    3. 第三
    1. 不需要数值递增
    1988. 😭
#####效果:
1. 第一
2. 第二
3. 第三
1. 不需要
1988. 数值递增

-----------------------
####8. 文字引用
    >文字引用

#####效果:
>这是文字的引用
>多写几行,文字的引用需要自己换行<br/>
>似水年华

---------------------
####9. 表示单行代码
    `code...`   //`code`(常见于键盘数字键1旁边,HHKB除外它在右上角)
        (这里有4个看不到的空格)code   //以四个空格或者Tab键开始的行,Tab将完全等同于4个空格,编辑器就是直接把Tab转换成的四个空格,两者本质上没有差别
#####效果:
`code...`
C++输出流 `cout<<"Hello world!"<<endl`

    code...
    System.out.println("Hello Java");

--------------------

####10. 加强的代码显示(MarkdownPad　免费版不支持代码块)
    ```普通代码
    $sudo git add .
    $git commit -m "msg"
    $git push -u origin master
    ```

#####效果:
```
$sudo git add .
$git commit -m "msg"
$git push -u origin master
```

C++示例
``` C++
#include<cstdio>
#include<iostream>
using namespace std;
int main()
{
    cout<<"hello world";
    system("pause");
    return 0;
}
```


JavaScript 示例：

``` javascript
/**
* nth element in the fibonacci series.
* @param n >= 0
* @return the nth element, >= 0.
*/
function fib(n) {
  var a = 1, b = 1;
  var tmp;
  while (--n >= 0) {
    tmp = a;
    a += b;
    b = tmp;
  }
  return a;
}

document.write(fib(10));
```

####11. Markdown中写注释
    目测写注释的唯一方法就是用<!-- -->了
    因为会转换成HTML代码
#####效果:
你好,世界
<!--你好,世界-->


------------------

Github Flavored Markdown介绍
================
[官网的帮助文档](https://help.github.com/articles/github-flavored-markdown)
####1. 换行
第一行
第二行
不用再打两个空格？
只是在机器认为了应该是两行的时候有效，比如下面的

Roses are red
Violets are blue

-------------
####2.改善斜体，避免和程序代码冲突

 `GFM ignores multiple underscores in words.  `
_text_
do_some_worry

------------------

####3.自动识别链接
https://yxjxx.me

-------------------
####4.文字中部划线的错误标注
GFM adds syntax to strikethrough text

    ~~Mistaken text~~

效果：
~~Mistaken text~~
####5. 支持语法高亮的代码块
Keep in mind that both types of code blocks need to have a blank line before them:

```
#sudo apt-get install gvim
#sudo apt-get install git
```

```c
#include<cstdio>
void main()
{
    printf("Hello world!\n");
}
```

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```
[查看github支持语法高亮的语言种类](https://github.com/github/linguist/blob/master/lib/linguist/languages.yml)

--------------------
####6. 任务列表（TaskList）

```
-[ ]First
-[x]Second
-[x]Third

```
效果：
-[ ]First
-[x]Second
-[x]Third

还有一些不那么常用的
####7. Quick quoting
####8. Name and Team @mentions autocomplete
####9. Emoji autocomplete
####10. Issue autocompletion
####11. Zen Mode (fullscreen) writing
####12. References

##说明

原文写作于2013年7月，2015年7月整理发布在我的个人 Wiki 上。现在 Mac 上涌现了一大批优秀的 Markdown 编辑器。

1. Mou
2. Ulysses
3. MacDown
4. Markdown Plus
5. Typora
6. Typed
7. iA Write Pro

最让人眼前一年的是 Typora ，它抛弃了左右双栏的传统形势，采用实时渲染的方式。很好的解决了 Markdown 中输入表格的难题。请看[少数派介绍文章](http://sspai.com/30292)。



