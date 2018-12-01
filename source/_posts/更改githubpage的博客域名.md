---
title: 更改githubpage的博客域名
date: 2016-12-26 22:30:56
tags:
categories: Others

---

# Godaddy端设置
在域名管理处，将你的域名，重定向连接到，你原有的githubpage的url:yourname.github.io.
由于在天朝，Godaddy默认的域名服务器在墙外，为了稳定，我们使用国内免费的DNSPOD的域名解析器,
在Godaddy域名服务器处添加两条记录f1g1ns1.dnspod.net和f1g1ns2.dnspod.net.
# DNSPOD端设置
ping username.github.io记录下IP地址，就是你要解析的博客地址.去DNSPod注册个账号，添加域名，设置两个A记录。分别是@和w w w，ip地址填上个步骤获取的IP地址.
激活启用新地址
# Hexo端设置
只在域名商处修改CNAME后，输入你设定的域名是会被导到你的Github pages页面没错，不过由于你的这个域名Github不知道，Github就会高冷地给你返回了一个404。其实Github很听话，你知道老实告诉它的‘新名字’就好了,在{your_hexo_folder}/source/下，创建一个名字为CNAME的文件，内容即是你的个人域名。hexo g,hexo d，渲染，部署到githubpage，等待使用新域名吧！
