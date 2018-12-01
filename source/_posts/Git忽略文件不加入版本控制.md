---
title: Git忽略文件不加入版本控制
date: 2017-02-01 17:21:48
tags: Git
---

## 共享式忽略

可以被git clone,只是是不在版本库里,比如说一些IDE的配置如果没有被.gitignore,可能会被别人merge什么的
新建 .gitignore 文件，放在工程目录任意位置即可。.gitignore 文件可以忽略自己
.gitignore文件可以被提交到共享库中被协作者共享


## 独享式忽略

文件彻底被排除,不会被版本控制,也不会被推送
.git/info/exclude


## 全局.gitignore

git 提供了一个全局的 .gitignore，你可以在你的用户目录下创建 ~/.gitignoreglobal 文件，以同样的规则来划定哪些文件是不需要版本控制的。
需要执行 git config --global core.excludesfile ~/.gitignoreglobal来使得它生效。

注意:
忽略的文件，只针对未跟踪文件有效，对已加入版本库的文件无效。要先 git rm -r ---cached ignore_file`

## .gitignore文件语法

```
#         #此为注释 – 将被 Git 忽略
*.a       # 忽略所有 .a 结尾的文件
!lib.a    # 但lib.a 除外
build/    # 忽略 build/整个build目录,但不包括同名文件,若想保留build空文件夹,改下方法，在build下也加一个.gitignore,内容为*!.gitignore
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO

     其他的一些过滤条件
    * ？：代表任意的一个字符
    * ＊：代表任意数目的字符
    * {!ab}：必须不是此类型
    * {ab,bb,cx}：代表ab,bb,cx中任一类型即可
    * [abc]：代表a,b,c中任一字符即可
    * [ ^abc]：代表必须不是a,b,c中任一字符
    ```

------

若test下有多个文件和文件夹。若要ignore某些文件夹，应该这个配置.gitignore文件。若test下有test1，test2,test3文件。要track test3，则.gitignore文件为：
test/test1
test/test2
!test/test3
若为：
test/
!test/test3 ，则不能track test3。

------
gitignore 还有个有意思的小功能， 一个空的 .gitignore 文件 可以当作是一个 placeholder 。当你需要为项目创建一个空的 log 目录时， 这就变的很有用。 你可以创建一个 log 目录 在里面放置一个空的 .gitignore 文件。这样当你 clone 这个 repo 的时候 git 会自动的创建好一个空的 log 目录了。---


## .gitignore文件参考
Python.gitignore
https://github.com/github/gitignore/blob/master/Python.gitignore
