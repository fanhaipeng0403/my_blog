---
title: tar命令
date: 2016-12-29 15:15:00
tags: Linux

---

Linux下tar命令exclude选项排除指定文件或目录
在linux中可以用tar打包目录以方便传输or备份，我们先来看一个例子
test 文件夹有如下文件
[root@lee ~]# ll test
总用量 8
-rw-r--r--. 1 root root    0 4月  14 22:18 a.jpg
-rw-r--r--. 1 root root    0 4月  14 22:25 a.log
-rw-r--r--. 1 root root    0 4月  14 22:18 a.txt
-rw-r--r--. 1 root root    0 4月  14 22:18 b.jpg
-rw-r--r--. 1 root root    0 4月  14 22:25 b.log
-rw-r--r--. 1 root root    0 4月  14 22:18 b.txt
drwxr-xr-x. 2 root root 4096 4月  14 22:18 dir1
drwxr-xr-x. 2 root root 4096 4月  14 22:18 dir2
打包
[root@lee ~]#  tar -cvf test.tgz test/

```
test/
test/b.jpg
test/b.txt
test/dir2/
test/b.log
test/dir1/
test/dir1/b.txt
test/dir1/a.txt
test/a.jpg
test/a.txt
test/a.log
```
这样是打包全部文件，我们需要排除jpg文件可以这么弄
[root@lee ~]#  tar -cvf test.tgz test/ --exclude *.jpg
```
test/
test/b.txt
test/dir2/
test/b.log
test/dir1/
test/dir1/b.txt
test/dir1/a.txt
test/a.txt
test/a.log
```
[root@lee ~]#
这样，就会把jpg后缀的文件都排除了，包括子目录！
如果是多个后缀类型需要被排除可以在后面添加，无限制
```
[root@lee ~]#  tar -cvf test.tgz test/ --exclude *.txt --exclude *.jpg
test/
test/dir2/
test/b.log
test/dir1/
test/a.log
[root@lee ~]#
```
以上是匹配排除某个文件类型后缀，也可以直接指定文件名
```
[root@lee ~]#  tar -cvf test.tgz test/ --exclude a.txt 
test/
test/b.jpg
test/b.txt
test/dir2/
test/b.log
test/dir1/
test/dir1/b.txt
test/a.jpg
test/a.log
[root@lee ~]#
```

或者指定目录

```
[root@lee ~]#  tar -cvf test.tgz test/ --exclude dir1
test/
test/b.jpg
test/b.txt
test/dir2/
test/b.log
test/a.jpg
test/a.txt
test/a.log
[root@lee ~]#
```
也可以排除目录与文件一起混合使用，如：
```
[root@lee ~]#  tar -cvf test.tgz test/ --exclude dir1 --exclude a.log --exclude *.jpg
test/
test/b.txt
test/dir2/
test/b.log
test/a.txt
```
