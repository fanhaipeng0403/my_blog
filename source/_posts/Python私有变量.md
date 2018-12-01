---
title: Python私有变量
date: 2017-02-18 16:51:16
tags:
---

## 保护型变量

_xx 以单下划线开头的表示的是protected类型的变量。即保护类型只能允许其本身与子类进行访问。若内部变量标示，如： 当使用“from M import”时，不会将以一个下划线开头的对象引入 。



## 私有变量

_\_xx 双下划线的表示的是私有类型的变量。只能允许这个类本身进行访问，连子类也不可以用于命名一个类属性（类变量），调用时名字被改变（在类FooBar内部，__boo变成_FooBar__boo,如self._FooBar__boo）

Python没有真正的私有变量。内部实现上，是将私有变量进程了转化，规则是：_<类名><私有变量>

下面的小技巧可以获取私有变量：

```
class Test(object):
     def __init__(self):
         self.__zzz=111

if __name__ == '__main__':
     a =  Test()
     print a._Test__zzz

```

同样，通过a._Test__zzz=222的方式，可以修改私有变量的值。

通过dir(Test)和dir(a)可以看到类属性和其实例属性之间的区别：


```
print dir(Test)
['__class__', '__delattr__', '__dict__', '__doc__', '__format__', '__getattribute__', '__hash__', '__init__', '__module__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__']
```

```
print dir(a)
['_Test__zzz', '__class__', '__delattr__', '__dict__', '__doc__', '__format__', '__getattribute__', '__hash__', '__init__', '__module__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__']
```

在这里强调说一下私有变量,python默认的成员函数和成员变量都是公开的,没有像其他类似语言的public,private等关键字修饰.但是可以在变量前面加上两个下划线"_",这样的话函数或变量就变成私有的

http://www.cnblogs.com/king-sun/p/4361998.html
