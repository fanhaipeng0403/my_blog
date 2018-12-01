---
title: Virtualenv
date: 2016-08-29 11:02:11
tags: Virtualenv

---

virtualenv用于创建独立的Python环境，多个Python相互独立，互不影响，它能够：

1. 在没有权限的情况下安装新套件
2. 不同应用可以使用不同的套件版本
3. 套件升级不影响其他应用

实际上就是不使用系统的包,自己另创建一个包管理文件夹,可以设置新建的包管理是否继承系统的包.


## 使用方法

sudo apt-get install python-virtualenv

virtualenv [虚拟环境名称]

virtualenv ENV

默认情况下，虚拟环境会依赖系统环境中的site packages，就是说系统中已经安装好的第三方package也会安装在虚拟环境中，如果不想依赖这些package，那么可以加上参数 --no-site-packages建立虚拟环境,

virtualenv --no-site-packages [虚拟环境名称]

启动虚拟环境

cd ENV
source ./bin/activate

注意此时命令行会多一个(ENV)，ENV为虚拟环境名称，接下来所有模块都只会安装到该目录中去。

退出虚拟环境

deactivate

在虚拟环境安装Python套件
Virtualenv 附带有pip安装工具，因此需要安装的套件可以直接运行：

pip install [套件名称]

如果没有启动虚拟环境，系统也安装了pip工具，那么套件将被安装在系统环境中，为了避免发生此事，可以在~/.bashrc文件中加上：
export PIP_REQUIRE_VIRTUALENV=true

或者让在执行pip的时候让系统自动开启虚拟环境：
export PIP_RESPECT_VIRTUALENV=true

## Virtualenvwrapper

Virtaulenvwrapper是virtualenv的扩展包，用于更方便管理虚拟环境，它可以做：
1. 将所有虚拟环境整合在一个目录下
2. 管理（新增，删除，复制）虚拟环境
3. 切换虚拟环境
4. ...

### 安装

sudo pip install virtualenvwrapper

此时还不能使用virtualenvwrapper，默认virtualenvwrapper安装在/usr/local/bin下面，实际上你需要运行virtualenvwrapper.sh文件才行，先别急，打开这个文件看看,里面有安装步骤，我们照着操作把环境设置好。

```
创建目录用来存放虚拟环境
mkdir $HOME/.virtualenvs

在~/.bashrc中添加行：
export WORKON_HOME=$HOME/.virtualenvs

在~/.bashrc中添加行：
source /usr/local/bin/virtualenvwrapper.sh  (如果你找不到virtualenvwrapper.sh这个文件,请参考http://stackoverflow.com/questions /12647266/where-is-virtualenvwrapper-sh-after-pip-install)

运行： source ~/.bashrc
```

此时virtualenvwrapper就可以使用了。

### 使用方法

所有的命令可使用：virtualenvwrapper --help 进行查看，这里列出几个常用的：

```
创建基本环境：
mkvirtualenv [环境名]

激活环境：
workon [环境名]

直接进入虚拟环境对应的目录:
cdvirtualenv

查看虚拟环境对应site-packages安装的包:
lssitepackages

退出环境：
deactivate

删除环境：
rmvirtualenv [环境名]

列出所有环境：
workon 或者 lsvirtualenv -b
```

### 指定虚环境python版本
$export VIRTUALENV_PYTHON=/opt/python-3.3/bin/python
$ virtualenv ENV
亦可
$ virtualenv --python=/opt/python-3.3/bin/python ENV

### 钩子
在你的虚拟环境工作目录有各种钩子命令,方便你定制命令.


## 一键安装 virtualenv,virtualenvwrapper
https://github.com/brainsik/virtualenv-burrito


