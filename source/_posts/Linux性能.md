---
title: Linux性能
date: 2016-08-05 00:01:17
tags: Linux

---
psdash 是一款查看 Linux 系统信息的 web 面板，和我们以前提到的另一款系统监控工具 Glances 一样，psDash 的系统信息的采集也是由 psutil 完成的。和 Glances 不同的是，psdash 没有提供 API，只带了一个基于 Flask 的 web 界面，默认每3秒刷新一次数据和界面。

升级系统后安装必要软件包：

$ sudo apt-get update
$ sudo apt-get upgrade

$ sudo apt-get install git gcc python-dev python-setuptools
下载 psdash 源代码后安装：

$ git clone https://github.com/Jahaja/psdash.git
$ cd psdash
$ sudo python setup.py install
启动 psdash：

$ sudo psdash --log /var/log/psdash.log --log /var/log/mydb.log
打开浏览器访问 http://192.168.2.99:5000/

![](http://www.vpsee.com/wp-content/uploads/2014/04/psdash.png)


https://github.com/Jahaja/psdash
http://www.open-open.com/lib/view/open1418873495027.html
http://www.cnblogs.com/lege/p/4228564.html


