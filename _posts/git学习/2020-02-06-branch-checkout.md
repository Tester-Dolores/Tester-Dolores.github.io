---
layout: post
title:  git branch & git checkout(分支管理 & 分支切换/撤销文件修改)
category: Git
tags: []
---
# git branch
## 本地分支

查看本地分支：`$ git branch`
查看远程分支：`$ git branch -r`
创建本地分支：`$ git branch [name] `----注意新分支创建后不会自动切换为当前分支

创建新分支并立即切换到新分支：`$ git checkout -b [name]`

删除分支：`$ git branch -d [name] `
-d选项只能删除已经参与了合并的分支，对于未有合并的分支是无法删除的。如果想强制删除一个分支，可以使用-D选项

合并分支：`$ git merge [name]`
将名称为[name]的分支与当前分支合并

## 远程分支

查看远程分支：`$ git branch -r`
创建远程分支(本地分支push到远程)：`$ git push origin [name]`
删除远程分支：`$ git push origin :heads/[name]` 或 `$ gitpush origin :[name]`

* 创建空的分支：(执行命令之前记得先提交你当前分支的修改，否则会被强制删干净没得后悔)

```
$git symbolic-ref HEAD refs/heads/[name]
$rm .git/index
$git clean -fdx
```

# git checkout 

切换分支：`$ git checkout [name]`
checkout：Git的checkout有两个作用，其一是在不同的branch之间进行切换，另一个功能是还原代码的作用，例如`git checkout app/model/user.rb`就会将user.rb文件从上一个已提交的版本中更新回来，未提交的内容全部会回滚

`git checkout -- readme.txt`

命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

* 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

* 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

**总之**，就是让这个文件回到最近一次git commit或git add时的状态。


[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help