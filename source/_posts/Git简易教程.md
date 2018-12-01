---
title: Git工作流程
date: 2017-01-17 13:41:40
tags: Git
---

![](https://pic4.zhimg.com/7e27e33239eeee59001da23a23483ccb_r.png)

- Git 鼓励用户大量使用分支,要在本地开发新功能,建立个分支;要合并个远程分支,建个分支先,总之避免在master上直接操作

- 推荐使用 git commit -v ,然后在打开的文件上方输入信息:

- gitmessage:

```
一个推荐的 commit message 应该是这样：

Redirect user to the requested page after login

https://trello.com/path/to/relevant/card

Users were being redirected to the home page after login, which is less
useful than redirecting to the page they had originally requested before
being redirected to the login form.

* Store requested path in a session variable
* Redirect to the stored location after successfully logging in the user
注释最好包含一个连接指向你们项目的 issue/story/card。一个完整的连接比一个 issue numbers 更好
提交信息中包含一个简短的故事，能让别人更容易理解你的项目
```
使用方式:

创建~/.gitmessage ,
然后在~/.gitconfig里面添加[commit]  template=~/.gitmessage



- . git 提供了一个全局的 .gitignore，你可以在你的用户目录下创建 ~/.gitignoreglobal 文件，执行 git config --global core.excludesfile ~/.gitignoreglobal来使得它生效。
对于 Python 可参考https://github.com/github/gitignore/blob/master/Python.gitignore

#　Git工作流程

## 在别人已有基础库上开发

```
git clone /path/to/repository  (git clone命令后我们会默认处于master分支下,并自动将origin设置为远程库表示)
如果是远端服务器上的仓库：git clone username@host:/path/to/repository

或者
git remote add origin gituser@git.server.com:project.git (先要ssh验证)
git pull


```
## 或者从头开始

```
git init
然后编写.gitignore文件
git add .
git commit -m "init project."
```


## 创建分支，修改代码,开始工作。


创建一个叫做“feature-A”的分支，并切换过去：

```
git checkout -b feature-A

亦可
git branch feature-A (默认从当前分支的head创建分支,你也可以指定)
git checkout feature-A
```


```
列出分支:
git branch
git branch -a  包括远程分支
重命名分支:
git branch -m new old_branch_name  new_branch_new
删除分支:
git branch -D branch_name
```


## 提交分支

```
git add <feature_filename>
git add *      提交到暂存区

------
你开发着,突然觉得方向错了:

从版本库恢复:
Git checkout --需要恢复的文件名

如果该文件已经 add 到暂存队列中，上面的命令就不灵光喽
需要先让这个文件取消暂存：

git reset HEAD --需要取消暂存的文件名
Git checkout --需要恢复的文件名
--------

git commit -v

一个推荐的 commit message 应该是这样：

Redirect user to the requested page after login

https://trello.com/path/to/relevant/card

Users were being redirected to the home page after login, which is less
useful than redirecting to the page they had originally requested before
being redirected to the login form.

* Store requested path in a session variable
* Redirect to the stored location after successfully logging in the user
注释最好包含一个连接指向你们项目的 issue/story/card。一个完整的连接比一个 issue numbers 更好
提交信息中包含一个简短的故事，能让别人更容易理解你的项目


```

## 开发过程中与主干同步

```

$ git fetch origin
$ git rebase origin/master


```

##  合并commit

```
git rebase -i origin/master
Pony Foo提出另外一种合并commit的简便方法，就是先撤销过去5个commit，然后再建一个新的。
$ git reset HEAD~5$ git add .$ git commit -am "Here's the bug fix that closes #28"$ git push --force
```

## 把服务器上最新版的代码fetch下来，然后跟自己的主分支合并。

```
git pull
首先切换的master分支：git checkout master。
然后执行合并操作：git merge --no-ff feature-A (--no--ff会让此次合并明确记录进log,建议这么做)
所有冲突解决后，git commit 提交更改。
http://www.yiibai.com/git/git_handling_conflicts.html
```
http://blog.csdn.net/wh_19910525/article/details/7554489
http://www.tuicool.com/articles/NzeQZz3




## 推送的远程库

```
再提交git push origin master

你还可以推送的远程库的特定分支:
先创建个本地分支,git checkout -b feature-C
然后git push -u origin feature-C (远程库有了feature-C分支)

对于你的同事来说
通过git branch -a
看到远程库的分支列表,
再通过git log origin/feature-C来仔细看你增加了什么新功能,
执行git checkout -b feature-C(可以是其他的名,这里是为了便于理解) origin/feature-C
和你一起培育此分支了

```

## 发出Pull Request

提交到远程仓库以后，就可以发出 Pull Request 到master分支，然后请求别人进行代码review，确认可以合并到master。



## 其他

可以通过git log 查看id，对库内的每一次提交打标签git tag
当我们需要删除暂存区或分支上的文件, 同时工作区也不需要这个文件了, 可以使用
git rm file_path
当我们需要删除暂存区或分支上的文件, 但本地又需要使用, 只是不希望这个文件被版本控制, 可以使用
git rm --cached file

# 其他使用总结


图像模式
git log --graph

简短的格式:
git log --oneline

完整模式
git log --prett=fuller
如何不仅想显示commit记录和hash,还是想看文件的修改记录:

git log -p <filename>

本地的分支已经提交A-> B-> C-> D和合并分支已提交A-> B-> X> Y，则Git合并将当前转换像这样的本地分行A-> B-> C-> D-> X-> Y
这个时候你只想看A-B-C-D
git log --no-merges master


## 修改你的提交


```
# 如果代码没有任何新变化，则用来改写上一次commit的提交信息
$ git commit --amend -m [message]

# 重做上一次commit，并包括指定文件的新变化
$ git commit --amend [file1] -m [message]

```

## 重置文件

在git中，有3种类型的重置。重置是让文件回到git历史中的一个特定版本。
git reset –hard {{some-commit-hash}} —— 回退到一个特定的历史版本。丢弃这次提交之后的所有变更。
git reset {{some-commit-hash}}—— 回滚到一个特定的历史版本。将这个版本之后的所有变更移动到“未暂存”的阶段。这也就意味着你需要运行 git add . 和 git commit 才能把这些变更提交到仓库.
git reset –soft {{some-commit-hash}} ——回滚到一个特定的历史版本。将这次提交之后所有的变更移动到暂存并准备提交阶段。意味着你只需要运行 git commit 就可以把这些变更提交到仓库。
这些命令似乎并没有什么用处，但当你尝试着将文件在不同版本间移动时，使用它们会非常方便。
我平时使用重置的一些用例如下：

如果想清除变更记录，可以使用清理命令——git reset –hard HEAD （最常用）
如果想编辑，以不同的顺序，重新暂存，重新提交文件—— git reset {{some-start-point-hash}}
git reset –soft {{some-start-point-hash}}如果想把之前3次的提交，作为一次提交 git reset –soft {{some-start-point-hash}}

##　二分法定位错误提交

git bisect



##  一次多处修改,分别提交
https://www.oschina.net/translate/10-tips-git-next-level?cmp

参考
http://blog.jobbole.com/96088/
http://blog.csdn.net/zxwd2015/article/details/51454668
http://www.bootcss.com/p/git-guide/
http://www.yiibai.com/git/home.html
https://pic4.zhimg.com/7e27e33239eeee59001da23a23483ccb_r.png
http://www.ruanyifeng.com/blog/2014/06/git_remote.html
http://www.ruanyifeng.com/blog/2015/08/git-use-process.html
http://www.ruanyifeng.com/blog/2015/12/git-workflow.html
http://www.ruanyifeng.com/blog/2015/08/git-use-process.html
