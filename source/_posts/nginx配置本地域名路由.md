
---
title: Nginx配置本地域名路由
date: 2017-09-17 15:14:50
tags: Nginx
---


## 处理过程


你在浏览器中 输入一个网址  会先check一下你本地的hosts 文件  如果有做映射的话 就直接通过映射的ip访问你的 web服务器（这边是nginx） 当这个请求被nginx 获得后  他会check一下请求的域名和servername是否匹配，匹配到的话 就根据相应的配置返回内容， 没有匹配到的话 就根据默认的配置返回内容。  

## 修改nginx.conf

```

server {
	listen 80;
	server_name www;
	location / {
		default_type text/html;
		content_by_lua '
			ngx.say("<p>first</p>")
		';
	}
}
 
server {
	listen  80;
	server_name www.zkh.com;
	location / {
		default_type text/html;
		content_by_lua '
			ngx.say("<p>second</p>")
		';        
	}
}
 
server {
	listen 80;
	server_name www.zkh.*;
	location / {
		default_type text/html;
		content_by_lua '
			ngx.say("<p>third</p>")
		';
 
	}
}
 
server {
	listen 80;
	server_name ~\w+.com;
	location / {
		default_type text/html;
		content_by_lua '
			ngx.say("<p>forth</p>")
		';        
	}
}
 
server {
	listen 80;
	server_name ~.*zkh.com;
	location / {
		default_type text/html;
		content_by_lua '
			ngx.say("<p>fifth</p>")
		';
	}


```


## 修改本地host文件

```
118.126.100.138 www.zkh.com
118.126.100.138 www.zkh.org
118.126.100.138 zkh.com
118.126.100.138 zkh.org



```


## 访问


![](https://img-blog.csdn.net/20181003105620903?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0NoZW5nX0tvaHVp/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

![](https://img-blog.csdn.net/20181003105644788?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0NoZW5nX0tvaHVp/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)


## 匹配顺序
server_name与host匹配优先级如下：

1. 完全匹配

2. 通配符在前的，如*.test.com

3. 在后的，如www.test.*

4. 正则匹配，如~^\.www\.test\.com$

如果都不匹配

1. 优先选择listen配置项后有default或default_server的

2. 找到匹配listen端口的第一个server块

 
