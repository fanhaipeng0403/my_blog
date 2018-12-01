---
title: Docker命令
date: 2017-02-03 18:13:09
tags:  Docker

---

Docker 是实现轻量级的操作系统虚拟化解决方案。用户操作 Docker 的容器就像操作一个快速轻量级的虚拟机一样简单。

# 基本概念

Docker 包括三个基本概念

- 镜像（Image）
- 容器（Container）
- 仓库（Repository）

----

镜像: 是一个只读的模板。可创建,可删除,可修改,可共享.

容器: 是从镜像创建的运行实例。每个容器都是相互隔离的、保证安全的平台。启动容器有两种方式，一种是基于镜像新建一个容器并启动，另外一个是将在终止状态（stopped）的容器重新启动。

仓库: 是集中存放镜像文件的场所。

仓库注册服务器上存放着多个仓库，每个仓库中又包含了多个镜像，每个镜像有不同的标签（tag）。

镜像有点像面向对象里的类,容器则是对应的一个实例,仓库是保存类的文件(类有不同的版本),仓库注册服务器是文件所在的计算机.

最大的公开仓库是 Docker Hub，存放了数量庞大的镜像供用户下载。

# 安装

更新源
sudo apt-get update

通过apt命令在线安装docker
sudo apt-get install docker-engine

开启docker的守护进程（Docker服务开启）
sudo service docker start

国际惯例，用一个Hello world的来测试安装成功
sudo docker run hello-world

更新Docker
sudo apt-get upgrade docker-engine

卸载Docker
sudo apt-get purge docker-engine
sudo rm -rf /var/lib/docker

创建Docker用户组,避免使用sudo
sudo usermod -aG docker user_name


# 镜像管理

```

搜索docker.hub中的镜像,无需登录
docker search  xxxx

sudo docker pull ubuntu:16.04
若不使用:tags那么tags默认为latest

docker images：
列出本地所有镜像

docker search <IMAGE_ID/NAME>：
查找image

docker pull <IMAGE_ID>：
下载image

docker push <IMAGE_ID>：
上传image

docker rmi <IMAGE_ID>：
删除image, 注意 docker rm 命令是移除容器。

sudo docker save -o XXXXXX.tar  <image_id>
保存镜像

docker load --input XXXXXX.tar
载入镜像


```
镜像使用
http://wiki.jikexueyuan.com/project/docker-technology-and-combat/create.html
http://www.runoob.com/docker/docker-image-usage.html


## 容器使用
```

查看:
docker ps

-a：同时显示停止的容器，默认只显示启动状态
-q：只显示容器id


------
使用:
docker start <CONTAINER_ID>：重新启动container
docker attach <CONTAINER_ID> 连接到启动的容器
要先启动,才能连接
docker stop <CONTAINER_ID>：停止container

------
监测:

docker inspect   <CONTAINER_ID>  容器底层信息
docker top   <CONTAINER_ID>成    容器进程信息
docker logs <CONTAINER_ID>  : 输出容器日志
docker logs -f <CONTAINER_ID> : 实时输出容器日志

------
导入导出:

docker export  <CONTAINER_ID> > xxxx.tar 导出容器
cat xxxx.tar | sudo docker import - ubuntu:v1.0 从容器快照导出为镜像

-----

```

如下

```
REPOSITORY      TAG                 IMAGE ID            CREATED              VIRTUAL SIZE
ubuntu         v1.0                9d37a6082e97        About a minute ago   171.3 MB
```

```
docker rm <CONTAINER_ID>：删除container ,如果要删除一个运行中的容器，可以添加 -f 参数。
docker rm `docker ps -a -q`：删除所有容器

docker cp <CONTAINER_ID>:path hostpath：复制容器内的文件到宿主机目录上

docker kill `docker ps -q`
docker rmi `docker images -q -a`
docker wait <CONTAINER_ID>：阻塞对容器的其他调用方法，直到容器停止后退出

docker top <CONTAINER_ID>：查看容器中运行的进程
docker diff <CONTAINER_ID>：查看容器中的变化
docker inspect <CONTAINER_ID>：查看容器详细信息（输出为Json）
-f：查找特定信息，如docker inspect -f '{{ .NetworkSettings.IPAddress }}'
docker commit -m "comment" -a "author" <CONTAINER_ID>  ouruser/imagename:tag
docker extc -it <CONTAINER> <COMMAND>：在容器里执行命令，并输出结果
```





# 容器管理

```
docker run  <IMAGE_ID>

-i：标准输入给容器
-t：分配一个虚拟终端
否则这样使用 docker run ubuntu:14.04 /bin/echo 'Hello world'
-d：以守护进程方式运行（后台）
--name： 指定容器的名称
--rm：退出时删除容器
```
docker run --name ovcer_the_container -i -t ubuntu /bin/bash
root@1ce9f640478d:/#
```
上面的命令将会创建一个名为ovcer_the_container的容器。对于一个合法的容器的名称来说只可以包括以下字符：小写字母a~z、大写字母A-Z、数字0～9、下划线、圆点、横线。

```




##　网络相关

```
默认匹配docker容器的5000端口号随机分配端口号
-P

查看容器的5000端口对应本地机器的IP和端口号,也可docker ps直接查看
docker port <CONTAINER_ID> 5000

指定端口号
-p <HOT_PORT>:<CONTAINER_PORT>

绑定主机的特定接口的端口号
docker run -p 127.0.0.1:5000:5000

绑定特定端口号（主机的所有网络接口的5000端口均绑定容器的5000端口）
docker run -p 5000:5000

绑定udp端口号
docker run -d -p 127.0.0.1:5000:5000/udp training/webapp python app.py：

查看映射端口配置
$docker port nostalgic_morse 5000
127.0.0.1:49155.
```


# 数据管理

数据卷是一个可供一个或多个容器使用的特殊目录，它绕过 UFS，可以提供很多有用的特性：
- 数据卷可以在容器之间共享和重用
- 对数据卷的修改会立马生效
- 对数据卷的更新，不会影响镜像

可以在容器启动的时候添加-v参数指定容器卷，也可以在Dockerfile里用VOLUMN命令添加

##  创建一个数据卷

在用 docker run 命令的时候，使用 -v 标记来创建一个数据卷并挂载到容器里。在一次 run 中多次使用可以挂载多个数据卷。
下面创建一个 web 容器，并加载一个数据卷到容器的 /webapp 目录。
sudo docker run -d -P --name web -v /webapp training/webapp python app.py
注意：也可以在 Dockerfile 中使用 VOLUME 来添加一个或者多个新的卷到由该镜像创建的任意容器。

##　挂载一个本地目录作为数据卷

sudo docker run -d -P --name web -v /src/webapp:/opt/webapp training/webapp python app.py
上面的命令加载主机的 /src/webapp 目录到容器的 /opt/webapp 目录。

## 挂载一个本地文件作为数据卷

sudo docker run -it -v ~/.bash_history:/.bash_history
这样就可以记录在容器输入过的命令了。

## 共享

在一个容器创建容器卷后，其他容器便可以通过--volumes-from共享这个容器卷数据，如下：

1. docker run -d -v /dbdata --name db1 training/postgres echo Data-only container for postgres
首先启动了一个d1容器，并为它增加一个数据卷/dbdata，然后启动另一个容器，共享这个数据卷

2. docker run -d --volumes-from db1 --name db2 training/postgres

此时容器db2使用了db1的容器卷，当容器db1被删除时，容器卷也不会被删除，只有所有容器不再使用此容器卷时，才会被删除
docker rm -v：删除容器卷

## 备份与恢复


### 备份

首先使用 --volumes-from 标记来创建一个加载 dbdata 容器卷的容器，并从本地主机挂载当前到容器的 /backup 目录。命令如下：
$ sudo docker run --volumes-from dbdata -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /dbdata
tar 命令来将 dbdata 卷备份为本地的 /backup/backup.tar。

### 恢复

如果要恢复数据到一个容器，首先创建一个带有数据卷的容器 dbdata2。
$ sudo docker run -v /dbdata --name dbdata2 ubuntu /bin/bash
然后创建另一个容器，挂载 dbdata2 的容器，并使用 untar 解压备份文件到挂载的容器卷中。
$ sudo docker run --volumes-from dbdata2 -v $(pwd):/backup busybox tar xvf  /backup/backup.tar

# 仓库管理

docker login：登录
本地用户目录的 .dockercfg 中将保存用户的认证信息。

http://www.myexception.cn/cloud/1787029.html


# 脚手架

## Docker Compose

允许用户在一个模板（YAML 格式）中定义一组相关联的应用容器（被称为一个 project，即项目），例如一个 Web 服务容器再加上后端的数据库服务容器等。
http://wiki.jikexueyuan.com/project/docker-technology-and-combat/fintro.html

## Docker Machine
Docker Machine是一个简化安装Docker环境的工具。市场上主流Linux系统版本很多，使用Machine工具就简单很多，一两条命令即可在主流Linux系统上安装Docker环境，用户不用考虑什么操作系统。Docker Machine还具备Docker工具管理虚拟化技术，Generic驱动默认管理LXC容器技术。
http://chuansong.me/n/341280351544

https://yeasy.gitbooks.io/docker_practice



