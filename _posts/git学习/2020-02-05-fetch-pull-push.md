---
layout: post
title:  git fetch & git pull & git push
category: Git
tags: []
---
远程主机名一般为origin,或者 为其他

# git fetch

`git fetch [远程主机名]  [BranchName]:[LocalBranchName]` 相当于是从远程获取master(BranchName)最新版本到本地分支，不会自动merge

如: `git fetch` //创建并更新本地远程分支
    `git fetch orgin`  //手动制定了远程主机,不指定分支时默认为master分支
　　`git fetch orgin master  ` //从远程获取master分支最新版本到本地分支
　　`git fetch orgin master:temp `  //从远程获取master分支最新版本到本地temp分支

`git log -p master  ..origin/master` //比较本地的master分支和origin/master分支的差别
`git merge origin/master `//进行合并远程仓库的master到本地
 
# git pull

`git pull [remoteName] [localBranchName] ` 等于是从远程获取最新版本并merge到本地分支

`git pull origin master `   //相当于git fetch 和 git merge

# git push
推送远程仓库：`$ git push [remoteName] [localBranchName]`
`$git push origin test:master` // 提交本地test分支作为远程的master分支
`$git push origin test:test` // 提交本地test分支作为远程的test分支

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help