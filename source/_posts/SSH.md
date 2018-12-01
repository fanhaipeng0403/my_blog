---
title: SSH
date: 2017-01-10 23:33:16
tags: Linux

---

Linux 下使用 ssh 登录局域网其他电脑的方法
首先查看电脑是否安装 ssh 客户端，如果没有执行下面命令安装客户端。

```
sudo apt-get install openssh-client
sudo apt-get install openssh-server
```

接着查看进程，看看 ssh-agent 是否运行，如果没有，输入下面指令启动 ssh 服务进程。

```
sudo service ssh start
```

关闭进程：

```
sudo service ssh stop
```


现在就可以用 ssh 远程登录到局域网内的电脑，指令格式：

```
ssh usr\@hostname
ssh usr\@ip
```

执行这个命令后会让你输入密码，只要输入 usr 的密码就行了。如果是首次连接，那么 Server 会问您，您的联机的 Key 尚未被建立，要不要接受 Server 传来的 Key ，并建立起联机呢？呵呵！这个时候请务必要输入 yes 而不是 y 或 Y，这样程序才会接受喔！

如果想删除通过 ssh 登录到主机上的一些用户可以使用下面命令：

```
pkill -kill -t pts/1
```

如果想进行文件的传输可以使用如下指令：

从机向主机传文件：
```
主机：nc -l [端口号] > 文件名
从机：nc [主机IP] [端口号] < 待传文件名
```


