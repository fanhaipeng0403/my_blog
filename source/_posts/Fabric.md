---
title: Fabric
date: 2016-12-29 10:24:22
tags: Deploy

---

[Fabric](http://fabric-chs.readthedocs.io/zh_CN/chs/tutorial.html)是一个 Python (2.5-2.7) 的库和命令行工具，用来提高基于 SSH 的应用部署和系统管理效率。利用Fabric部署Python、Ruby、PHP这样的非编译型网站应用非常方便，而对于编译型的Java、C#等就麻烦了，编译本身就是一个极其复杂的大工程，需要依赖特定工具或者IDE，很难做到自动化。
http://fabric-docs-cn.readthedocs.io/zh_CN/latest/
[安装](http://fabric-chs.readthedocs.io/zh_CN/chs/running_tests.html)

### Fabric的基本操作命令

Fabric支持的常用命令列出如下：
1. local
Run a command on the local system.
它是对subprocess模块的封装（Shell=True）可以通过设置Capture = True/False来捕获其执行结果。
2. run
Run a shell command on a remote host.
该命令的返回值包含了远程命令是否执行成功以及远程命令的返回码等信息。通过run执行命令时，通常会要求输入目标机器密码，如果对多台机器进行部署，可以通过设置env.passwords来避免手动输入密码，具体的设置方法会在下篇笔记中介绍。
3. get
Download one or more files from a remote host.
4. put
Upload one or more files to a remote host.
5. sudo
Run a shell command on a remote host, with superuser privileges.
功能与run操作类似，它可以对当前用户临时提权来执行某些需要root权限的命令。
此外，还有些不常用的命令（如：prompt, reboot, open_shell, require）这里没有列出


<!--more-->


### Task

在fabric中，一组具有逻辑关系的操作通常被封装成一个task，fabric以task为粒度来执行命令，下面开始介绍如何定义task

#### 脚本名称与位置

- 基于fabric的部署脚本通常以fabfile.py命名且应该位于当期工作目录下以便于fab进行搜索，在该文件中实现我们想要的任务即可。当然，如果要实现的部署任务比较复杂，这些任务也可以写在多个脚本中，统一置于fabric package下。放置位置在根目录：

```
|-- __init__.py
|-- app.wsgi
|-- fabfile.py <-- our fabfile!
|-- manage.py
`-- my_app
    |-- __init__.py
    |-- models.py
    |-- templates
    |   `-- index.html
    |-- tests.py
    |-- urls.py
    `-- views.py
```

若不以fabfile.py命名,在创建它后输入 fab -f fab_tasks.py <task name> ，或者在 ~/.fabricrc 中添加 fabfile = fab_tasks.py 。

#### 定义task

```
@taskdef deploy(environment, domain="whatever.com"):
    run("git clone foo")
    sudo("service apache2 restart")
```


#### 为task指定目标机器

**env.hosts**和**env.roles**可以用来全局指定task的目标机器列表，这两个“环境变量”的默认值都是空列表[]。

##### env.hosts

```
env.hosts = ['host1', 'host2']
def taskA():
    run('ls')
def taskB():
    run('whoami')
```

##### env.roles

env.roles则是在配置了env.roledefs的情况下才有用武之地。在很多时候，不同的机器有着不同的角色，如有些是接入层，有些是业务层，有些是数据存储层。env.roledefs可以用来组织这些机器列表以体现其角色，示例如下：

```

from fabric.api import env

env.roledefs = {    'web': {
                 'hosts': ['www1', 'www2', 'www3'],
    },           'db': {
                 'hosts': ['db1', 'db2'],
    }
}

@roles('web')
def mytask():
    run('ls /var/www')
```

上例通过env.roledefs配置了两个角色web和db，分别包含3台、2台机器，并借助@roles为mytask指定了目标机器列表。


##### 在命令行指定

```
 fab -H host1,host2 mytask1
```

但这样操作，mytask只会在host1, host2上执行

如若

```
env.hosts.extend(['host3', 'host4'])
def mytask():
    run('ls /var/www')123456
```

此时，当我们运行”fab -H host1,host2 mytask”时，env.hosts包含来自命令行和fabfile的4台机器。

##### 为每个任务指定host

借助装饰器@hosts为每个任务指定目标机器


```
from fabric.api import env, run

env.hosts.extend(['host3', 'host4'])
def mytask():
    run('ls /var/www'）


   ##or#
my_hosts = ('host1', 'host2')
@hosts(my_hosts)
def mytask():
    # ...

```



### 目标机器的密码管理

如果不想每次都输入SSH密码，需要事先在目标机器上生成ssh public key并配置在~/.ssh/config文件中，然后在定义任务的fabfile中将env.use_ssh_config设置为True,
来启用基于ssh public key方式的身份认证

可以参考这篇文章,[SSH参考](http://www.ruanyifeng.com/blog/2011/12/ssh_remote_login.html)

### 其他

[彩色输出](http://fabric-chs.readthedocs.io/zh_CN/chs/api/core/colors.html)
运行”fab –list”来查看fabric可以识别的任务
http://www.liaoxuefeng.com/article/001373892650475818672edc83c4c978a45195eab8dc753000

### 注意事项

1. 开发 Fabric 时，最好建立一个独立的 virtualenv 环境来安装依赖并运行测试。
2. 建议使用

```
from fabric.api import *
```
导入API,虽然不符合最佳规范，但是fabric本身也没多少API,不会和本地命名空间产生冲突，所以这样更为实用。

3. 对于run命令注意

```
run('cd /home/work/tmp')
run('mkdir test')
```

第2次run会重新创建ssh连接，且不会记忆上次cd到的目录

需要用下面的命令来实现：

```
run('cd /home/work/tmp; mkdir test')
run('cd /home/work/tmp && mkdir test')
```

但建议更好的方式:


```
with cd('/home/work/tmp'):
    run('mkdir test')
```



### 例子


```
#!/usr/bin/env python
#-*- coding: utf-8 -*-

from datetime import datetime
from fabric.api import *

#登录用户和主机名：
env.user = 'root'
env.hosts = ['www.example.com'] # 如果有多个主机，fabric会自动依次部署

def pack():
    ' 定义一个pack任务 '
    # 打一个tar包：
    tar_files = ['*.py', 'static/*', 'templates/*', 'favicon.ico']
    local('rm -f example.tar.gz')
    local('tar -czvf example.tar.gz --exclude=\'*.tar.gz\' --exclude=\'fabfile.py\' %s' % ' '.join(tar_files))

def deploy():
    ' 定义一个部署任务 '
    # 远程服务器的临时文件：
    remote_tmp_tar = '/tmp/example.tar.gz'
    tag = datetime.now().strftime('%y.%m.%d_%H.%M.%S')
    run('rm -f %s' % remote_tmp_tar)
    # 上传tar文件至远程服务器：
    put('shici.tar.gz', remote_tmp_tar)
    # 解压：
    remote_dist_dir = '/srv/www.example.com@%s' % tag
    remote_dist_link = '/srv/www.example.com'
    run('mkdir %s' % remote_dist_dir)
    with cd(remote_dist_dir):
        run('tar -xzvf %s' % remote_tmp_tar)
    # 设定新目录的www-data权限:
    run('chown -R www-data:www-data %s' % remote_dist_dir)
    # 删除旧的软链接：
    run('rm -f %s' % remote_dist_link)
    # 创建新的软链接指向新部署的目录：
    run('ln -s %s %s' % (remote_dist_dir, remote_dist_link))
    run('chown -R www-data:www-data %s' % remote_dist_link)
    # 重启fastcgi：
    fcgi = '/etc/init.d/py-fastcgi'
    with settings(warn_only=True):
        run('%s stop' % fcgi)
    run('%s start' % fcgi)
```


-------
```
from __future__ import with_statement
from fabric.api import *
from fabric.contrib.console import confirm

env.hosts = ['my_server']

def test():
    with settings(warn_only=True):
        result = local('./manage.py test my_app', capture=True)
    if result.failed and not confirm("Tests failed. Continue anyway?"):  # 这有个短逻辑
      
        abort("Aborting at user request.")

def commit():
    local("git add -p && git commit")

def push():
    local("git push")

def prepare_deploy():
    test()
    commit()
    push()

def deploy():
    code_dir = '/srv/django/myproject'
    with settings(warn_only=True):
        if run("test -d %s" % code_dir).failed:
            run("git clone user@vcshost:/path/to/repo/.git %s" % code_dir)
    with cd(code_dir):
        run("git pull")
        run("touch app.wsgi")
```
