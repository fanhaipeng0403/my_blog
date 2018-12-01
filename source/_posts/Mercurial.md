---
title: Mercurial
date: 2017-02-10 14:06:41
tags:  Ubuntu
---


今天想看在一个网站看https://bitbucket.org/leafstorm/ryshcate/src/c828fd08ad241756502124602e6a1196e862f1d1/ryshcate/?at=default项目的源码,知道了一个叫hg的版本控制工具,安装如下

Mercurial 是强大的分布式版本控制系统. 本文将介绍如何在 Ubuntu 下快速的最新版的安装Mercurial, 其实只要几条命令就可以搞定了.


sudo add-apt-repository ppa:tortoisehg-ppa/releases
sudo add-apt-repository ppa:mercurial-ppa/releases
sudo apt-get update
sudo apt-get install mercurial python-nautilus tortoisehg


