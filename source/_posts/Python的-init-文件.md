---
title: Python的__init__文件
date: 2017-02-16 23:03:29
tags: Python

---


## 将包等效于模块,__init__文件的内容就是你想对外公开的包内容 , 即__init__.py 文件定义了包的属性和方法。

```
your_package/
  __init__.py
  file1.py/
  file2.py/
    ...
  fileN.py

# in __init__.py
from file1 import *
from file2 import *
...
from fileN import *

# in file1.py
def add():
    pass

包外模块如果想引用add

可以直接
from your_package import add
```


## 包外模块找到包内的特定对象

```
可以
from your_package.file1 import add
但是,建议不要这样导入,想让add暴露给其他模块,就放到__init__.py文件
```

##  初始化配置的作用

因为一个包也是对象，所以它也可以初始化。python类有__init__方法作为初始化函数，包自然也有__init__.py来实现初始化

```
import logging.config
logging.config.dictConfig(Your_logging_config)
```

## 导入路径

1. 当前目录
2.  sys.path
3. site-packages

#导入方法

举个例子, 目录结构如下, 
-cake
|- __init__.py
|- icing.py
|- sponge.py
-drink
|- __init__.py
|- water.py

在 sponge.py 引用 icing , 有多种方法: * import icing # implicit relative import, py2已强烈不推荐使用, py3已经不可用了 * from . import icing # explicit relative import, python.org 官方虽不推荐, 但这却是事实标准 * from cake import icing # absolute import , python 官方推荐.



#　总结:

1.  PEP338推荐,绝对引用,尤其再main主文件,必须绝对引用,但是有时候绝对引用,不利于修改,而且名字比较长

2.  显示相对引用,也已经成为实时标准,用的很多

3.  隐式相对(就是根据当前,标准,第三方目录等顺序),不推荐使用

推荐看这篇文件
https://my.oschina.net/leopardsaga/blog/97175




