---
title: Git Rebase
date: 2017-09-17 15:14:50
tags: Git
---

https://www.jianshu.com/p/5c9c6383aa36﻿


# 变基

总的原则是，只对尚未推送或分享给别人的本地修改执行变基操作清理历史，从不对已推送至别处的提交执行变基操作.


## 开发合并别人的分支，保存图谱干净

* 在dev1分支上进行开发，然后commit提交，在dev1分支上生成一个提交单。
* 切换到master分支，与remote/master分支同步。
* 切换回dev1分支，将master分支rebase到dev1分支上，如果有冲突，修改冲突。rebase操作的冲突修改与merge不一样，修改完冲突后，保存进index（ c），然后直接git rebase --continue即可，不同再多做一次提交。
* 切换回master分支，合并dev1分支，此时合并会非常顺畅。然后push。



```

mkdir test1
cd test1

echo 1 > file
git add .
git commit -m '1'

git checkout -b dev
echo 2 >> file
git  add .
git commit -m  '2'

git checkout  master
git pull origin master


git checkout  dev
git rebase master

# fix config

git add .
git rebase --continue

git checkout master
git merge dev

```



## 回退每个commit


1. 找到要回退的commit的**前一个commit的**hash值

2. git rebase -i commit_hash

3. 交互界面出现这个hash值之后的所有commit记录，pick-->drop, 丢弃你不想要的commit

4. git rebase --continue





