---
title: Session
date: 2017-01-21 23:47:04
tags: Web

---

Session Cookies Cache 的区别

Session 是单用户的会话状态。当用户访问网站时，产生一个 sessionid。并存在于 cookies中。每次向服务器请求时，发送这个 cookies，再从服务器中检索是否有这个 sessionid保存的数据；

Cookie同session一样是保存你个人信息的，不过是保存在客户端，也就是你使用的电脑上，并且不会被丢掉，除非你删除浏览器Cookie；

而 cache ，则是服务器端的缓存，是所有用户都可以访问和共享的，因为从Cache中读数据比较快，所有有些系统（网站）会把一些经常被使用的数据放到Cache里，提高访问速度，优化系统性能
