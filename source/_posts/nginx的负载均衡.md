---
title: Nginx负载均衡
date: 2017-10-17 15:14:50
tags: Nginx
---

转发的文章 https://www.shixinke.com/nginx/nginx-upstream

一、什么是负载均衡？
根据一定的规则将请求分发到不同的服务器上，让各个服务器分摊请求，而不是让一台服务器来处理请求

传统的请求过程

使用负载均衡：


好处：减轻同一台服务器的压力，提高服务器的响应速度

二、nginx实现负载均衡？
(一)upstream的用法
1、upstream
作用：是用来定义服务器组的模块

使用范围：proxy_pass、fastcgi_pass、memcached_pass等

结构：

upstream groupName {
    server serverName1 [param1=value1] [param2=value2] [param3];
    server serverName2;
}
groupName即为组名，是自定义的,如：upstream webserver;

2、server
upstream中的server用来指定一个服务器。

server的类型可以是：

(1)域名：如:webserver.website.com;

(2)IP：如:192.168.0.239:80;

(3)Unix套接字文件：如unix:/tmp/webserver;

例如：

upstream webserver {
     server httpweb.withec.com;
     server 192.168.18.201 weight=5 max_fails=3 fail_timeout=20s;
     server 192.168.18.202 backup;
     server 192.168.18.293 down;
     server unix:/tmp/httpdweb;
}
server中可用的参数：

(1)weight:表示权重，权重越大，表示被访问的概率越大
用法：weight=数字；

server 192.168.18.201 weight=4;
(2)max_fails：表示连接失败重新连接的最多次数
用法：max_fails=3;

如：

server 192.168.18.202 max_fails=3;
(3)fail_timeout:连接超时的时间(即多久算连接失败)
用法：fail_timeout=时间;

如：20秒就算连接失败

server 192.168.18.202 max_fails=3 fail_timeout=20s;
(4)backup:标记一台服务器作为备用服务器(它只在其他服务器繁忙的时候工作)
用法：server serverName backup;

如：

server 192.168.18.203 backup;
(5)down:标记一台服务器下线或者暂时不可用
用法：server serverName down;

如：

server 192.168.18.203 down;
(6)max_conns:表示指定的服务器最大连接数限制(nginx1.5.9以上版本才有的参数)
用法：max_conns=数字;

如：

server 192.168.18.202 max_conns=1024;
(二)、upstream实验：
4台机器：

IP:192.168.18.200(作前端服务器)

192.168.18.201

192.168.18.202

192.168.18.203

步骤：

1、三台机器上的nginx都需要启动，并在各自web根目录下的index.html的文件中加入机器识别信息，具体如下：

200的机器上的index.html添加：from 200

201的机器上的index.html,添加：from 201

202的机器上的index.html,添加：from 202

203的机器上的index.html,添加：form 203

2、在237的机器上配置nginx

(1)在http块中加入：

upstream webserver {
      server 192.168.18.201:80;
      server 192.168.18.202:80;
      server 192.168.18.203:80;
}
       (2)在server区段的location段加入：

location / {
    proxy_pass http://webserver;
}
注：webserver这个组名前一定要记住加http://

打开浏览器访问：http://192.168.18.200，查看显示内容

发现显示”from 201”

刷新显示”from 202”

再刷新显示”from 203”

再刷新显示””from 201

依次刷新会在这三台机器之间循环(这种专业的叫法叫轮询)

(三)upstream模块主要指令
1、hash:指定轮询的规则按照指定的key值来计算
用法：hash key;

这个key可以包含文本，变量或者文本与变量的组合。

2、ip_hash;指定轮询的规则按照ip的hash值来计算
针对上面的实验：我们在upstream中加入ip_hash，再查看：

发现我们无论怎么刷新，访问的都是201上面的文件(因为客户端的IP没变)



更多的指令可以参考nginx官方文档：

http://nginx.org/cn/docs/http/ngx_http_upstream_module.html

(如果不喜欢看英文文档，可以看中文文档)

http://nginx.org/cn/docs/http/ngx_http_upstream_module.html