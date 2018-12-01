---
title:  Python相对导入中Attempted relative import in non-package问题
date: 2017-01-30 22:58:15
tags:  Python

---


问题描述
目录结构：

```
dev@desktop:~/Desktop/test$ ls
controller.py __init__.py test.py
```

文件内容:

```
dev@desktop:~/Desktop/test$ cat controller.py 
class Controller:
    def __init__(self):
        pass
dev@desktop:~/Desktop/test$ cat __init__.py 
# -*- coding: utf-8 -*-
dev@desktop:~/Desktop/test$ cat test.py 
# !/usr/bin/env python
from .controller import Controller 
if __name__ == '__main__':
    print('running...')
出现的错误：
在运行test.py程序时显示在非包目录中试图进行相对导入
```
```
dev@desktop:~/Desktop/test$ python3 test.py 
Traceback (most recent call last):
  File "test.py", line 2, in <module>
    from .controller import Controller 
ValueError: Attempted relative import in non-package
```
问题原因
不能在一个包里运行一个脚本文件，顶层的脚本文件不能用相对导入。
如果要将一个包作为一个脚本运行的话，需要将运行的脚本文件更名为__main__.py，然后再该包文件夹外运行该包的命令:

python -m testpackage
还有一种解决办法是在包外创建一个脚本文件，然后将包的内容导入到该脚本中。

http://blog.jasonding.top/2015/02/03/Python/%E3%80%90python%E3%80%91%E7%9B%B8%E5%AF%B9%E5%AF%BC%E5%85%A5%E4%B8%ADAttempted-relative-import-in-non-package%E9%97%AE%E9%A2%98/
http://wiki.jikexueyuan.com/project/python3-cookbook/module-and-pack.html
