---
title: Django_Models
date: 2017-02-06 18:32:52
tags:  Django

---

# Django 的 ORM 有多种关系：一对一，多对一，多对多。

各自定义的方式为 ：

- OneToOneField

一对一,一个有一个，即 has one：

- ForeignKey，

多个属于一个, lots of A belong to B
一个有很多个， has many: B has many A
在建立 ForeignKey 时，另一个表会自动建立对应的关系

- ManyToManyField

多对多,一个既有很多个，又属于很多个，即 has many, belong to Many
在建立ManyToManyField时，另一个表会自动建立对应的关系


## OneToOneField Example


```
from django.db import models

class Engine(models.Model):
    name = models.CharField(max_length=25)

    def __unicode__(self):
        return self.name

class Car(models.Model):
    name = models.CharField(max_length=25)
    #  这个车的引擎的name可以在表Engine的name中找到,同时也能从引擎的name找到这两车
    engine = models.OneToOneField(Engine)

    def __unicode__(self):
        return self.name

>>> from testapp.models import Car, Engine
>>> e = Engine.objects.get(name='Diesel')

# Engine 的model 定义中并没有car，这个是自动生成的，**用关联表的类名小写直接访问**

>>> e.car
<Car: Audi> # 返回的使用一个可调用的对象
>>> c = Car.objects.get(name='Audi')
```

## ForeignKey with unique=True Example

```
class Engine2(models.Model):
    name = models.CharField(max_length=25)

    def __unicode__(self):
        return self.name

class Car2(models.Model):
    name = models.CharField(max_length=25)
    # 这个车的引擎的name可以在Engine2中name找到,同时Engine2的引擎有很多车用
    engine = models.ForeignKey(Engine2, unique=True)

    def __unicode__(self):

>>> from testapp.models import Car2, Engine2
>>> c2 = Car2.objects.get(name='Mazda')
>>> e2 = Engine2.objects.get(name='Wankel')

# 用了这个引擎的所有车

>>> e2.car2_set.all()
[<Car2: Mazda>]  # 处理的是QuerySet而不是模型实例
# 在未定义的model中用关联表类名小写加"_set"来访问，这里是car2_set,多对多也一样
# Engine2 的model 定义中并没有car2，这个是自动生成的

```


```
from django.db import models

class Publisher(models.Model):
    name = models.CharField(max_length=30)
    address = models.CharField(max_length=50)
    city = models.CharField(max_length=60)
    state_province = models.CharField(max_length=30)
    country = models.CharField(max_length=50)
    website = models.URLField()

    def __unicode__(self):
        return self.name

class Author(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=40)
    email = models.EmailField()

    def __unicode__(self):
        return u'%s %s' % (self.first_name, self.last_name)

class Book(models.Model):
    title = models.CharField(max_length=100)
# 一本书有很多作者,一个作者也可能有很多书
    authors = models.ManyToManyField(Author)
# 一本书属于出版社,一个出版社可以出很多书
    publisher = models.ForeignKey(Publisher)
    publication_date = models.DateField()

    def __unicode__(self):
        return self.title

上面定义了Publisher，Author，Book三个类，按照“每个数据库表对应一个类”的“原则”，执行python manage.py syncdb 应该创建三个表，但你可以看到（创建的时候就有打印显示）数据库里多了一个表（四个表）名为：book_authors ，这就是那个“额外的表”，是因为“多对多”字段的原因创建的。
Chai 2014-02-07 16:21:57
多对多关系是没法用字段来表示的，需要用额外的一张表来维护多对多关系。

------
表内字段

>>> from mysite.books.models import Book
>>> b = Book.objects.get(id=50)
>>> b.title
u'The Django Book'

-------

外键,一对多(多对一)

从belong to 的关系来看

>>> b = Book.objects.get(id=50)
>>> b.publisher
<Publisher: Apress Publishing>
>>> b.publisher.website
u'http://www.apress.com/'

从has many 的关系来看

>>> p = Publisher.objects.get(name='Apress Publishing')
>>> p.book_set.all()
[<Book: The Django Book>, <Book: Dive Into Python>, ...]

实际上，book_set 只是一个 QuerySet，所以它可以像QuerySet一样,能实现数据过滤和分切，例如：

>>> p = Publisher.objects.get(name='Apress Publishing')
>>> p.book_set.filter(name__icontains='django')
[<Book: The Django Book>, <Book: Pro Django>]

属性名称book_set是由模型名称的小写(如book)加_set组成的。

------
多对多

>>> b = Book.objects.get(id=50)
书籍的所有作者
>>> b.authors.all()
[<Author: Adrian Holovaty>, <Author: Jacob Kaplan-Moss>]
>>> b.authors.filter(first_name='Adrian')
[<Author: Adrian Holovaty>]
>>> b.authors.filter(first_name='Adam')

反向查询也可以。

作者的所有书
>>> a = Author.objects.get(first_name='Adrian', last_name='Holovaty')
>>> a.book_set.all()
[<Book: The Django Book>, <Book: Adrian's Other Book>]

```

其他:
- Model操作
http://djangobook.py3k.cn/2.0/chapter05/
- 对于pycharm用户可以使用UML图来查看不同表之间的关系


```
Python3兼容Python2

from django.utils.encoding import python_2_unicode_compatible
 
@python_2_unicode_compatible
class Article(models.Model):
    title = models.CharField('标题', max_length=256)
    content = models.TextField('内容')
 
    pub_date = models.DateTimeField('发表时间', auto_now_add=True, editable = True)
    update_time = models.DateTimeField('更新时间',auto_now=True, null=True)
 
    def __str__(self):
        return self.title
```
