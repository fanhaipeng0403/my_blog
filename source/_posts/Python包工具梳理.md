---
title: Python包工具梳理
date: 2017-02-10 19:52:17
tags: Python

---

# distutils 是 python 标准库的一部分，这个库的目的是为开发者提供一种方便的打包方式， 同时为使用者提供方便的安装方式。

假设目录创建三个文件foo.py、bar.py和setup.py

```
from distutils.core import setup
setup(
    name='fooBar',
    version='1.0',
    author='Will',
    author_email='wilber@sh.com',
    url='http://www.cnblogs.com/wilber2013/',
    py_modules=['foo', 'bar'],
)
```

在该目录中运行 python setup.py sdist ，会得到以下输出，同时生成了一个"fooBar-1.0.zip"包。

甚至能打包成 rpm 或者 exe 安装包：

```
python setup.py bdist_rpm
python setup.py bdist_wininst
```

<!--more-->

使用者就可以解压缩这个包然后执行 python setup.py install进行安装，然后就可以使用foo、bar这两个模块了

# setuptools/distribute 都扩展了 distutils，提供了更多的功能, 它们是同一个东西。

```
#!/usr/bin/env python
from setuptools import setup, find_packages

with open('requirements.txt') as f:
    requirements = f.read().splitlines()

setup(
    name='sopy',
    version='1.7',
    packages=find_packages(),
    include_package_data=True,
    url='http://sopython.com/',
    license='BSD',
    author='David Lord',
    author_email='davidism@gmail.com',
    description='The productive programming cabbage website.',
    entry_points={'console_scripts': ['sopy = sopy.manage:cli.main']},
    install_requires=requirements
)

```

在 setup.py 中，也存在一个 install_requires 表来指定依赖的安装。

```
#!/usr/bin/env python
from setuptools import setup

setup(
    name='hive-executor-py',
    version='1.0.0.dev1',
    description='A hive client python project',
    url='https://github.com/calvinjiang/hive-executor-py',
    author='Calvin Jiang',
    author_email='jianghuachinacom@163.com',
    license='MIT',
    classifiers=[
        'Development Status :: 4 - Beta',
        'Intended Audience :: Developers',
        'Topic :: Software Development :: Build Tools',
        'License :: OSI Approved :: MIT License',
        'Programming Language :: Python :: 2.6',
        'Programming Language :: Python :: 2.7',
        'Programming Language :: Python :: 3',
        'Programming Language :: Python :: 3.3',
        'Programming Language :: Python :: 3.4',
        'Programming Language :: Python :: 3.5',
    ],
    keywords='hive client python',
    packages=['hive'],
)
name为项目名称，和顶层目录名称一致;
version是项目当前的版本，1.0.0.dev1表示1.0.0版，目前还处于开发阶段
description是包的简单描述，这个包是做什么的
url为项目访问地址，我的项目放在github上。
author为项目开发人员名称
author_email为项目开发人员联系邮件
license为本项目遵循的授权许可
classifiers有很多设置，具体内容可以参考官方文档
keywords是本项目的关键词，理解为标签
packages是本项目包含哪些包,我这里只有一个名词为hive的包
```


Eggs 格式是 setuptools 引入的一种文件格式，它使用 .egg 扩展名，用于 Python 模块的安装。


wheel 本质上是一个 zip 包格式，它使用 .whl 扩展名，用于 python 模块的安装，它的出现是为了替代 Eggs。

wheel 还提供了一个 bdist_wheel 作为 setuptools 的扩展命令，这个命令可以用来生成 wheel 包。

easy_install是基于setuptools/distribute的一个工具，方便了包的安装和省级


- 从PyPI上安装一个包：

当使用 easy_install package 命令后，easy_install 可以自动从 PyPI 上下载相关的包，并完成安装，升级

- 下载一个包安装：

通过 easy_install package.tgz 命令可以安装一个已经下载的包

- 安装egg文件：

通过 easy_install package.egg 可以安装一个egg格式的文件


# pip是目前最流行的Python包管理工具，它被当作easy_install的替代品，但是仍有大量的功能建立在setuptools之上。

pip 希望不再使用 Eggs 格式（虽然它支持 Eggs），而更希望采用“源码发行版”（使用 python setup.py sdist 创建）。

pip 可以利用 requirments.txt 来实现在依赖的安装。

pip 提供了一个 wheel 子命令来安装 wheel 包。当然，需要先安装 wheel 模块。



# 总结:


## 打包发布

Setuptools

```
python setup.py --help-commands    21:02:46  ☁  master ☀
Standard commands:
  build             build everything needed to install
  build_py          "build" pure Python modules (copy to build directory)
  build_ext         build C/C++ extensions (compile/link to build directory)
  build_clib        build C/C++ libraries used by Python extensions
  build_scripts     "build" scripts (copy and fixup #! line)
  clean             clean up temporary files from 'build' command
  install           install everything from build directory
  install_lib       install all Python modules (extensions and pure Python)
  install_headers   install C/C++ header files
  install_scripts   install scripts (Python or otherwise)
  install_data      install data files
  sdist             create a source distribution (tarball, zip file, etc.)
  register          register the distribution with the Python package index
  bdist             create a built (binary) distribution
  bdist_dumb        create a "dumb" built distribution
  bdist_rpm         create an RPM distribution
  bdist_wininst     create an executable installer for MS Windows
  upload            upload binary package to PyPI
  check             perform some checks on the package

Extra commands:
  saveopts          save supplied options to setup.cfg or other config file
  compile_catalog   compile message catalogs to binary MO files
  develop           install package in 'development mode'
  upload_docs       Upload documentation to PyPI
  extract_messages  extract localizable strings from the project code
  init_catalog      create a new catalog based on a POT file
  test              run unit tests after in-place build
  update_catalog    update message catalogs from a POT file
  setopt            set an option in setup.cfg or another config file
  install_egg_info  Install an .egg-info directory for the package
  rotate            delete older distributions, keeping N newest files
  bdist_wheel       create a wheel distribution
  egg_info          create a distribution's .egg-info directory
  alias             define a shortcut to invoke one or more commands
  easy_install      Find/get/install Python packages
  bdist_egg         create an "egg" distribution
  build_sphinx      Build Sphinx documentation

usage: setup.py [global_opts] cmd1 [cmd1_opts] [cmd2 [cmd2_opts] ...]
   or: setup.py --help [cmd1 cmd2 ...]
   or: setup.py --help-commands
   or: setup.py cmd --help
```

关于打包文件格式:

一开始distutils是python steup.py sdit,打包成zip或tar.gz格式
然后setuptools出现了eggs格式,再后来wheel格式想替他eggs格式
pip支持wheel,(需要安装wheel模块),不在支持eggs(原来eggs用esay_install安装)

所以,推荐使用wheel格式

## 安装

pip


# 打包发布到PyPi

## 注册PyPi账号,创建文件

在您的本机用户下创建~/.pypirc文件
```
[distutils]
index-servers = pypi

[pypi]
username:jianghua
```

##  注册你的项目

```
python setup.py register
```

这个时候你可以在PyPi网站看到自己的项目名称了


## 上传项目

```
python setup.py sdist bdist_wheel upload

sdist             create a source distribution (tarball, zip file, etc.)
bdist_wheel       create a wheel distribution

```

# 其他:

## 打包为可执行文件以便分发。

PyInstaller – 将 Python 程序转换成独立的执行文件（跨平台）。
dh-virtualenv – 构建并将 virtualenv 虚拟环境作为一个 Debian 包来发布。
Nuitka – 将脚本、模块、包编译成可执行文件或扩展模块。
py2app – 将 Python 脚本变为独立软件包（Mac OS X）。
py2exe – 将 Python 脚本变为独立软件包（Windows）。
pynsist – 一个用来创建 Windows 安装程序的工具，可以在安装程序中打包 Python本身。

## 构建工具

buildout – 一个构建系统，从多个组件来创建，组装和部署应用。
BitBake – 针对嵌入式 Linux 的类似 make 的构建工具。
fabricate – 对任何语言自动找到依赖关系的构建工具。
PlatformIO – 多平台命令行构建工具。
PyBuilder – 纯 Python 实现的持续化构建工具。
SCons – 软件构建工具。


https://packaging.python.org/
https://www.zhihu.com/question/24590883
http://zengrong.net/post/2169.htm
http://blog.csdn.net/lynn_kong/article/details/17540207
