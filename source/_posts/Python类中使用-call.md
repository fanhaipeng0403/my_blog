---
title: Python类中使用__call__
date: 2017-06-04 19:47:39
tags: Python
---

对象通过提供__call__(slef, [,*args [,**kwargs]])方法可以模拟函数的行为，如果一个对象x提供了该方法，就可以像函数一样使用它，也就是说x(arg1, arg2...) 等同于调用x.__call__(self, arg1, arg2) 。  模拟函数的对象可以用于创建防函数(functor) 或代理(proxy)
```
class DistanceForm(object):
    def __init__(self, origin):
        self.origin = origin
        print "origin :"+str(origin)
    def __call__(self, x):
        print "x :"+str(x)
 
p = DistanceForm(100)
p(2000)
 
输出
>>> 
origin :100
x :2000
```
