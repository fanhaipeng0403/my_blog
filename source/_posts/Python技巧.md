---
title: Python实践
date: 2016-07-02 12:47:09
tags: Python

---
最佳实践文档
https://gist.github.com/sloria/7001839
https://gist.github.com/JeffPaine/6213790
```
1.如何使用PIP更新package？

python -m pip install --upgrade package_name




2.如何判断文件是否存在？

import os.path

os.path.isfile(filename)




3.Python中的三元运算符

a if test else b

根据test为True，则返回a，若为False，则返回b




4.如何在一个表达式里合并两个字典？

>>> x = {'a':1, 'b': 2}

>>> y = {'b':10, 'c': 11}
>>> z = dict(x.items() + y.items())

>>> z

{'a': 1, 'c': 11, 'b': 10}




5.如何用字典的值对字典进行排序？

import operator

x ={1: 2, 3: 4, 4:3, 2:1, 0:0}

sorted_x = sorted(x.items(),key = operator.itemgetter(1)) 或者

sorted(d.items(), key=lambda x: x[1])




6.如何在一个函数里用全局变量?

如果我在一个函数里建了一个全局变量,那么我怎么在另一个函数里使用这个全局变量?

我需要把这个全局变量赋值给这个函数的局部变量吗?

如果你要在别的函数里使用全局变量,只要在被调用全局变量函数的里事先用global声明一下:

globvar = 0

def set_globvar_to_one():

global globvar # 需要用global修饰一下globvar

globvar = 1

def print_globvar():

print globvar # 如果要读globbar的值的话不需要用global修饰

set_globvar_to_one()

print_globvar() # 输出 1

我猜正是因为全局变量比较危险,所以Python为了确保你真的知道它是全局变量,所以需要加一个global关键字.




7.检查列表是否为空的最好方法？

if not a:

print "List is empty"

用隐藏的空列表的布尔值才是最Pythonic的方法.




8.__str__和repr__的区别？


- 用起来没有什么区别

- __repr__的目的是明确的

- __str__的目的是可读性

- __str__的用法包含__repr__

a='a\nb'
In [2]:

print str(a)
a
b
In [3]:

print repr(a)
'a\nb'




9.在循环中获取索引(数组下标)？

list_test = [8, 23, 45, 12, 78]

for index, value in enumerate(list_test):

print index , value




10.Python中的append和extend的区别？

In[7]: x = [1,2,3,4]

In[8]: y = [8,9,10]

In[9]: x.append(y)

In[10]: x

Out[10]: [1, 2, 3, 4, [8, 9, 10]]

In[11]: x = [1,2,3,4]

In[12]: y = [8,9,10]

In[13]: x.extend(y)

In[14]: x

Out[14]: [1, 2, 3, 4, 8, 9, 10]




10.字典里添加元素的方法?

In[15]: x  = {1:2,3:4}

In[16]: x.update({5:6})

In[17]: x

Out[17]: {1: 2, 3: 4, 5: 6}




11.Python中有检查字符串包含的方法吗?

if not "haha" in sstring: continue

或者:

if "haha" not in somestring : continue




12.如何在只用一行捕获多个异常？

try:

something

except(ExceptionA,ExceptionB,.....) as e:

something




13.在Python里怎么读取stdin?

import fileinput

for line in fileinput.input():

pass




14.在Python里获取当前时间?

In[19]: import datetime

In[20]: datetime.datetime.now()

Out[20]: datetime.datetime(2016, 5, 26, 11, 31, 55, 508000)

In[21]: datetime.datetime.now().time()

Out[21]: datetime.time(11, 32, 5, 775000)




15.在Python怎么样才能把列表分割成同样大小的块?

tuple(l[i:i+n] for i in xrange(0, len(l), n))




16.检查一个字符串是否是一个数字?

In[22]: x = '569789'

In[23]: x.isdigit()

Out[23]: True

In[24]: y = 'gdf2667'

In[25]: y.isdigit()

Out[25]: False




17.查找列表中某个元素的下标?

In[26]: ['a','b','c'].index('b')

Out[26]: 1




18.如何在列表中随机取一个元素？

import random

f= ['a', 'b', 'c']

print(random.choice(f))




19.字典推倒式

d = {key: value for (key, value) in iterable}




20.如何最快速反转字符串？

In[30]: 'nihao ma'[::-1]

Out[30]: 'am oahin'




20.如何测量脚本的运行时间？

Python自带了一个叫cProfile的分析器.它不仅实现了计算整个时间,而且单独计算每个函数运行时间,并且告诉你这个函数被调用多少次,它可以很容易的确定你要优化的值.

你可以这样调用：

import cProfile

cProfile.run('foo()')

In[37]: import cProfile

In[38]: cProfile.run('fm()')

4950

3 function calls in 0.000 seconds

Ordered by: standard name

ncalls  tottime  percall  cumtime  percall filename:lineno(function)

1    0.000    0.000    0.000    0.000 :1(fm)

1    0.000    0.000    0.000    0.000 :1()

1    0.000    0.000    0.000    0.000 {method 'disable' of '_lsprof.Profiler' objects}




21.Python中用什么代替switch语句?

在其他语言中有switch语句，但是python中没有。可以用字典的方式来解决这个问题。

def helpFunction(x):

return {

'a':12,

'b':45,

'c':78

}[x]

if __name__=='__main__':

print helpFunction('b')

如果你希望设置一个默认值可以用字典的get方法:

def f(x):

return {

'a': 1,

'b': 2,

}.get(x, 9)




22.如何生成包含大写字母和数字的随机字符串？

In[40]: import random

In[41]: import string

In[42]: ''.join(random.choice(string.ascii_uppercase+string.digits) for _ in range(5))

Out[42]: 'XBNH7'




23.如何合并两个列表？

list1 = [1,2,3,4]

list2 = [5,6,7,8]

list3 = list1+list2




24.如何把字符串转化为时间？

from datetime import datetime

date_object = datetime.strptime('Jun 1 2016 1:33PM', '%b %d %Y %I:%M%p')

Out[45]: datetime.datetime(2016, 6, 1, 13, 33)




25.如何用pip升级所有包？

pip freeze --local | grep -v '^\-e' | cut -d = -f 1 | xargs pip install -U




26.如何给字符串填充0？

A = 'demo'

A.rjust(5,'0')

'0demo'

```
