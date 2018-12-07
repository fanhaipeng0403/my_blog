---
title: node.js
date: 2017-01-12 16:54:17
tags: Node.js

---

nodejs - 如何完全更新

Nodejs可以毫不犹豫地说一个版本狂魔，时不时就发布一个版本，而且还一直没有一个1.0版本，好囧呀，对于我们这些有强迫症的人来说，的确不是好事。

下面我就说一下Nodejs中常见的更新方式。

1. 更新你已经安装的NPM库，这个很简单，只需要运行。

npm update –g
2. 更新Nodejs自身。一直依赖我都是下载最新版的源码，然后make install，及其繁琐。其实只需要运行以下2个命令即可：

npm install –g n
n latest
n可以下载任意版本的nodejs安装到本机，非常方便。

