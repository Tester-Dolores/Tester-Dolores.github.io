---
layout: post
title:  Github Page & Jekyll 搭建博客
category: 随笔
tags: [学习笔记]
---

<p>https://sharefs.yun.kugou.com/202008030050/6f3e60d91e216b702cda820f8dc827f7/G213/M05/08/11/tZQEAF6muvKAIEkAAEBqH0VZabA093.mp3</p>
搭建blog纯属心血来潮,看到github上许多牛人分享了自己的博客,又看看自己现在在其他平台的blog,搞一个吧!

历经几天(家里网速实在是太慢了,download rubyinstall 实在是不行,没法最后去其他地方download)总算是搞好了环境,fork别人的模板,开始认真的写作了!

环境: Win10 x64 

## 1.下载 rubyinstaller
官网: https://rubyinstaller.org/downloads/

这里我下载的是 Ruby+Devkit 2.6.X (x64)

全程傻瓜式安装 - 注意不要**取消勾选**加入环境变量选项

安装成功后会自动打开一个类似命令行窗口, 输入 3 ,按enter继续,最后再按enter继续.

最后检查是否安装成功

ruby -v

gem -v

## 2.安装bundler & jekyll
首先我们改一下gem源,否则你会遇到报错!(原因看这里-> https://gems.ruby-china.com/)

` gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/ `

安装bundler: `gem install bundler`

安装jekyll: `gem install jekyll`

## 3.启动服务
`jekyll server`,启动成功后浏览器打开 http://127.0.0.1:4000/


## 4.搭建博客

1.你必须有github账号

2.你必须创建一个repositories  或者 直接fork别人的项目,到setting里面把Repository name改为你的user_name.github.io**(必须是user_name)**

3.你可以搭建git环境, 用来push代码.(如果不嫌麻烦,也可以直接在github更改),据说一个小时push不能超过10次.

4.学习一下markdown语法

5.学习一下jekyll语法


ps:我这里是fork别人的项目,但 是,我当时不知道可以直接用,所以我用git 克隆下来,然后放到我自己创建的repositories,然后 更改相关的配置.然后push上去.

## 5.搭建博客遇到的问题

### First question: 日期被自动加1天
**解决方法:**

修改博客时间 添加 +0800

`date:   2020-07-31 22:21:49 +0800`

### Second question: 404


https://zhuanlan.zhihu.com/p/97340941   JeKyll 在 Windows 下本地预览中文路径

https://github.com/Huxpro/huxpro.github.io/issues/62   run jekyll serve failed ''cannot load such file -- jekyll-paginate

**解决方法:**

1.找到 ruby安装路径\Ruby26-x64\lib\ruby\2.6.0\webrick\httpservlet\filehandler.rb,添加两行代码

```
/*第一处*/
path = req.path_info.dup.force_encoding(Encoding.find("filesystem")
path.force_encoding("UTF-8") # 加入的代码
if trailing_pathsep?(req.path_info)  

/*第二处*/
break if base == "/"
base.force_encoding("UTF-8") # 加入的代码
break unless File.directory?(File.expand_path(res.filename + base))
```

2.重启jekyll

`jekyll clean && jekyll serve`


本以为到此就完美解决问题了,结果又又又报错了!抓狂....

```
Configuration file: D:/Tester-Dolores.github.io/_config.yml
jekyll 4.1.1 | Error:  cannot load such file -- D:/NEWdownload/rubyinstaller-devkit-2.6.6-1-x64/Ruby26-x64/lib/ruby/gems/2.6.0/gems/tzinfo-data-1.2020.1/lib/tzinfo/data/definitions/CN
```

解决方法: 重装依赖

Just two step:"First run 'gem uninstall --all', then run 'gem install github-pages'"

OK! 完美解决!

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
