---
title: 上传代码到github及所出现的问题
date: 2018-08-24 14:28:44
tags: [github]
---

## 上传github所发现的问题 

**准备工作**

使用git bush 输入下面的命令

```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

**上传代码到github的步骤：**

参考[两种方法上传本地文件到github](https://www.jianshu.com/p/c70ca3a02087)

 1. 新建一个文件夹 ，放入需要上传的代码文件
 2. 使用 git 进入到该文件夹下
 3. 执行  `git init`
 4. 执行 `git add .` 
 5. 执行  `git commit -m "upload"`
 6. 执行  `git remote  add origin  https://github.com/yourname/yourrepository`
 7. 执行 `git push -u origin master`

**使用 git push -u origin master 出现的问题**
```
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'git@github.com:zweros/DataStructure.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

```
然后按照网上的文章说 git pull origin master


**使用 git pull origin master 发现的问题**

```
*branch master -> FETCH_HEAD

fatal: refusing to merge unrelated histories

```
**解决方案**

[参考stackoverflow](https://stackoverflow.com/questions/50111060/fatal-refusing-to-merge-unrelated-histories-after-adding-git-remote)
```
You need to either `reset` or `commit` your changes first:

    git reset --hard

or:

    git commit -m "saving changes..."

Then you can do:

    git pull origin master --allow-unrelated-histories
```

**最后终于能上传成功了**

```shell
$ git push -u origin master
Enumerating objects: 204, done.
Counting objects: 100% (204/204), done.
Delta compression using up to 4 threads.
Compressing objects: 100% (91/91), done.
Writing objects: 100% (203/203), 2.65 MiB | 21.00 KiB/s, done.
Total 203 (delta 111), reused 202 (delta 111)
remote: Resolving deltas: 100% (111/111), done.
To github.com:zweros/DataStructure.git
   7838db7..e4721c9  master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

```