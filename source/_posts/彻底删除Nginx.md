---
title: Nginx
date: 2016-09-30 18:48:48
tags: Nginx
---


##  彻底删除
1.先执行一下命令：
sudo apt-get --purge remove nginx
sudo apt-get autoremove
dpkg --get-selections|grep nginx
罗列出与nginx相关的软件， nginx-common deinstall 然后
sudo apt-get --purge remove nginx-common
这样就可以完全卸载掉nginx包括配置文件
2.ps -ef |grep nginx 看下nginx还有没有启动,一般执行完1后，nginx还是启动着的，如下：
bkxmgx@ubuntu:/$ ps -ef |grep nginx
root     4061  2418  0 Mar11 ?        00:00:00 nginx: master processsbin/nginx
nobody   4062  4061  0 Mar11 ?        00:00:00 nginx: worker process
bkxmgx  15487  4229  0 01:13 pts/0    00:00:00 grep --color=auto nginx
3.kill   nginx进程
sudo kill -9  4061  4062

4.sudo  find  / -name  nginx*
/usr/local/src/nginx-1.7.9
/usr/local/src/nginx-1.7.9/objs/src/core/nginx.o
/usr/local/src/nginx-1.7.9/objs/nginx.8
/usr/local/src/nginx-1.7.9/objs/nginx
/usr/local/src/nginx-1.7.9/src/http/modules/perl/nginx.xs
/usr/local/src/nginx-1.7.9/src/http/modules/perl/nginx.pm
/usr/local/src/nginx-1.7.9/src/core/nginx.c
/usr/local/src/nginx-1.7.9/src/core/nginx.h
/usr/local/src/nginx-1.7.9/man/nginx.8
/usr/local/src/nginx-1.7.9/conf/nginx.conf
/usr/local/src/nginx-1.7.9/contrib/vim/syntax/nginx.vim
/usr/local/src/nginx-1.7.9/contrib/vim/ftdetect/nginx.vim
/usr/local/src/nginx-1.7.9/contrib/vim/indent/nginx.vim
/usr/local/nginx
/usr/local/nginx/logs/nginx.pid
/usr/local/nginx/conf/nginx.conf.default
/usr/local/nginx/conf/nginx.conf
/usr/local/nginx/sbin/nginx
/home/bkxmgx/nginx.conf
/home/bkxmgx/nginx-1.7.9.tar.gz
/home/bkxmgx/桌面/nginx.conf
/home/bkxmgx/桌面/nginx~
/home/bkxmgx/桌面/nginx

5.依依删除4列出的所有文件
sudo rm  -r  /usr/local/src/nginx-1.7.9
sudo rm  -r  /usr/local/nginx
sudo rm  -r  /usr/local/nginx/logs/nginx.pid
sudo rm  -r  /usr/local/nginx/conf/nginx.conf.default
sudo rm  -r  /usr/local/nginx/conf/nginx.conf
sudo rm  -r  /usr/local/nginx/sbin/nginx
sudo rm  -r  /home/bkxmgx/nginx.conf
sudo rm  -r  /home/bkxmgx/桌面/nginx.conf
sudo rm  -r  /home/bkxmgx/桌面/nginx~
sudo rm  -r  /home/bkxmgx/桌面/nginx

这样就彻底删除nginx了


## 卸载apache

所以先卸载apache2，不然你在访问服务器的时候会一直是apache2 的页面
http://www.linuxidc.com/Linux/2013-06/85825.htm



## Nginx安装

安装Nginx

（1）在线安装

$sudo apt-get install nginx

Nginx的版本是1.2.1

ubuntu安装Nginx之后的文件结构大致为：

所有的配置文件都在/etc/nginx下，并且每个虚拟主机已经安排在了/etc/nginx/sites-available下

启动程序文件在/usr/sbin/nginx

日志放在了/var/log/nginx中，分别是access.log和error.log

并已经在/etc/init.d/下创建了启动脚本nginx

默认的虚拟主机的目录设置在了/usr/share/nginx/www

## 启动Nginx

（1）在线安装的启动过程

$sudo /etc/init.d/nginx start

（2）源代码安装的启动过程

$cd /usr/local/nginx

$sbin/nginx

然后就可以访问了，http://localhost/ ， 一切正常！如果不能访问，先不要继续，看看是什么原因，

解决之后再继续。

如果你的机器同时安装了Apache，那上面的访问方式就不能使用了，而且nginx都可能启动不了，这是因为它们都是用了80这个端口。我们这里将nginx的端口修改为8080，

使用apt-get安装的nginx配置文件为： /etc/nginx/sites-available/default，可以用sudo vim /etc/nginx/sites-available/default命令打开。看到如：server {
listen 80;

其中，listen 80;指的是监听80端口。只需修改为listen 8080即可。

说明：修改端口后，在输入网址时需指定端口号，如localhost:8080，否则显示错误。而默认的80端口在输入网址时可以省略（往往不加上去）。

然后就可以访问了，http://localhost:8080/ 。



http://www.ziqiangxuetang.com/django/django-nginx-deploy.html
http://chenpeng.info/html/3472
http://www.mamicode.com/info-detail-1370140.html
