---
layout: post
title:  Path配置pipenv ~/.bashrc
category: Git
tags: []
---

source: https://www.cnblogs.com/hizf/p/7843463.html
```
sudo apt install python3.7
pip3 install pipenv
```

![](https://img2020.cnblogs.com/blog/826848/202011/826848-20201104144147133-616664946.png)


`PATH=~/.local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin `               # 配置pipenv路径                          

`PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin  `      #未配置pipenv路径

 

**Linux：`/bin;/sbin;/usr/bin;/usr/sbin;/usr/local/bin;/usr/local/sbin`的意义**

原文 source:https://blog.csdn.net/test1280/article/details/70143465      

 `/bin`：通常是普通用户和超级用户都会用到的必要的命令，例如ls，pwd等等

`/sbin`：通常是系统管理员使用的必要的来管理系统的命令，例如shutdown，ifconfig等等。

**注：**sbin意义为system binary。

`/usr/bin`：通常是一些非必要的，但是普通用户和超级用户都可能使用到的命令，例如gcc，ldd等等。

**注：**很多时候我们自己安装的软件，可能在此处建立一个软连接（符号链接），指向实际的可执行文件。

`/usr/sbin`：通常是一些非必要的，由系统管理员来使用的管理系统的命令，例如crond，httpd等等。

**注：**这里面有很多类似httpd等这样的后台程序，主要是提供一些服务，有相当一部分是关于网络的（并不全是，例如crond），这个时候这个进程就是作为一个“服务器”，接受外部的请求。

`/usr/local/bin`：通常是用户后来安装的软件，可能被普通用户或超级用户使用。

`/usr/local/sbin`：通常是用户后来安装的软件，一般是用来管理系统的，被系统管理员使用。

从用户权限角度来看，*sbin下的命令都是用来管理系统的，所以一般是普通用户无法执行，只有系统管理员可以执行，而`*bin`下的命令则是所有用户都可以执行的。

**注：**以上所说的并不是绝对的，例如ifconfig在`/sbin`下，但是普通用户一般具有可执行权限。


配置,可在任意路径执行pipenv

![](https://img2020.cnblogs.com/blog/826848/202011/826848-20201104144204974-1806931876.png)


未配置,不可执行
![](https://img2020.cnblogs.com/blog/826848/202011/826848-20201104144220243-1633756526.png)


**上面的内容，主要还是一些知识点整理和个人的一些思考，权当参考，如有错误或者更好的建议，可以在评论区指正，不胜感激！**


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

