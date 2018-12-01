---
title: Ubuntu系统崩溃问题
date: 2017-02-17 16:14:18
tags: Ubuntu
---

今天电脑强制关机,再开机的时候,出现了initramfs问题,搞了半天,终于修好了,记录一些:

```
输入fsck -y /dev/sda2  (sda2根据你自身情况决定) ,修复grub
输入exit退出,可登陆系统,但是之后重启还会出现之前的问题

在登录系统时,进入终端,输入
sudo gedit /etc/default/grub
找到
GRUB_CMDLINE_LINUX_DEFAULT=”quiet splash”
修改为
GRUB_CMDLINE_LINUX_DEFAULT=”rootdelay=60 quiet splash”
```
