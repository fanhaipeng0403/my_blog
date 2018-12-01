---
title: Python的__str__
date: 2017-03-04 08:13:51
tags: Python
---

__str__           直接打印对象的实现方法
————————————————————————————————————————————————————
在python语言里，__str__一般是格式是这样的。
class A:
def __str__(self):
return "this is in str"
事实上，__str__是被print函数调用的，一般都是return一个什么东西。这个东西应该是以字符串的形式表现的。如果不是要用str()函数转换。当你打印一个类的时候，那么print首先调用的就是类里面的定义的__str__,比如：str.py
#!/usr/bin/env python
                                                                                                                                                                                 
class strtest:
    def __init__(self):
        print "init: this is only test"
    def __str__(self):
        return "str: this is only test"

if __name__ == "__main__":
    st=strtest()
    print st

$./str.py
init: this is only test
str: this is only test
从上面例子可以看出，当打印strtest的一个实例st的时候，__str__函数被调用到。
其实，python里面的对象基本上都默认有个__str__供print函数所用。比如字典里的__str__,见红色部分：
>>> dir({})
['__class__', '__cmp__', '__contains__', '__delattr__', '__delitem__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__len__', '__lt__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'clear', 'copy', 'fromkeys', 'get', 'has_key', 'items', 'iteritems', 'iterkeys', 'itervalues', 'keys', 'pop', 'popitem', 'setdefault', 'update', 'values']
>>> t={}
>>> t['1'] = "hello"
>>> t['2'] = "world"
>>> t   #等于 print t
{'1': 'hello', '2': 'world'}
>>> t.__str__()
"{'1': 'hello', '2': 'world'}"
大家可以看到一个字典，print t 和 t.__str__()是一样的。只不过__str__()将字典内容以字符串形式输出。
看看下面的例子，如果在函数__str__里返回的不是字符串，请看str1.py
#!/us/bin/env/python                                                                                                                                                                                        
#__metaclass__ = type
#if __name__ == "__main__":
class strtest:
    def __init__(self):
        self.val = 1
    def __str__(self):
        return self.val

if __name__ == "__main__":
    st=strtest()
    print st

$./str1.py
Traceback (most recent call last):
  File "./str.py", line 12, in <module>
    print st
TypeError: __str__ returned non-string (type int)
错误的信息提示：__str__返回了一个非字符串。这时候我们应该这样做：请看str2.py
#!/usr/bin/env python                                                                                                                                                                                        
#__metaclass__ = type
#if __name__ == "__main__":
class strtest:
    def __init__(self):
        self.val = 1
    def __str__(self):
        return str(self.val)

if __name__ == "__main__":
    st=strtest()
    print st

$./str2.py
1
我们用str()将整型变为了字符型。


http://blog.csdn.net/followingturing/article/details/7954204
