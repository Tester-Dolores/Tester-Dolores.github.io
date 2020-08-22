---
layout: post
title:  git status &git diff &git log (暂存区状态 & 查看区别 & 查看commit日志)
category: Git
tags: []
---

# git log :查看提交日志

　　`git log --pretty=oneline` 查看提交日志(只打印commit id和描述)

 
# git status  : 时刻掌握仓库当前的状态
 
```
$ git status

On branch master

Changes not staged for commit:

  (use "git add <file>..." to update what will be committed)

  (use "git checkout -- <file>..." to discard changes in working directory)

 

modified:   readme.txt

 

no changes added to commit (use "git add" and/or "git commit -a")
```
 
`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。

 
```
$ git status

On branch master

Changes to be committed:

  (use "git reset HEAD <file>..." to unstage)

 

modified:   readme.txt
```

`git status`告诉我们，将要被提交的修改包括readme.txt，下一步，就可以放心地提交了

 
```
$ git status

On branch master

nothing to commit, working tree clean
```

Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working tree clean）的

一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的

可以用git log查看提交日志

***

# git diff: 顾名思义就是查看difference

　　git diff HEAD -- readme.tx   可以查看工作区和版本库里面最新版本的区别
```

$ git diff readme.txt 

diff --git a/readme.txt b/readme.txt

index 46d49bf..9247db6 100644

--- a/readme.txt

+++ b/readme.txt

@@ -1,2 +1,2 @@

-Git is a version control system.

+Git is a distributed version control system.

 Git is free software.
```

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help