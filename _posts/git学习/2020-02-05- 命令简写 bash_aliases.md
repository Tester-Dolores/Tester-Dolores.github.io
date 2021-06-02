---
layout: post
title:  命令简写 ~/.bash_aliases
category: Git
tags: []
---

原文source:https://www.linuxidc.com/Linux/2014-10/107547.htm

`~/.bashrc`文件默认有对`~/.bash_aliases`的引用,但是默认情况下该文件不存在!

使用`sudo nano ~/.bashrc `进入查看文件内容

![](https://img2020.cnblogs.com/blog/826848/202011/826848-20201104145320135-298432283.png)


创建文件`:touch filename `即`touch  ~/.bash_aliases`

`sudo nano  ~/.bash_aliases`

将简写命令写入,格式如下:

`alias 简写命令='全写命令'`

注意等号左右不能有空格！

 

**保存后需要重新开启ubuntu才会生效!**

**上面的内容，主要还是一些知识点整理和个人的一些思考，权当参考，如有错误或者更好的建议，可以在评论区指正，不胜感激！**


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

