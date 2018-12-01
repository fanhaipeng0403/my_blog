---
title: Xpath
date: 2016-06-17 16:54:29
tags: Python

---
## 介绍

Xpath是一门语言,专门用于解析xml和html
Xpath相比于正则表达式更简易好,正则表达式是告诉计算机寻找特定样子的字符串,而xpath
是直接告诉计算机寻找某个节点

配合requests库使用,requests库相比于urllib2更人性化

-----
## 基本使用

安装lxml库
from lxml import etree
selector = etree.Html
seletor.xpath(规则)

import sys
reload(sys)
sys.setdefaultencodeing('utf-8')

------

##　规则的获取

chrome 选择元素然后copyxpath
- // 定位根节点
- / 往下寻找
- 提取文本内容:/text()
- 提取属性内容:/@xxxx

//url[@id='useful']/li/text()
//div/url[@id='useful']/li/text()
//a/@href
//div[starts-with(@id,'test')]/text()

-------
##　多线程
map函数一手包办了序列操作，参数传递和结果保存等一系操作
from multiprocessing.dummy import Pool
pool=Pool(你的cpu核数) # 生产线程池
result=pool.map(爬虫函数,网址序列)

```
from mutiprocssing.dummy import Pool as ThreaPoll
import requests
import time

def getsource(url)
   html=requests.get(url)

url=[]

for i in range(1,21):
    newpage='http://tieba.com/p/35223957?pn'+str(i)
    urla.append(newpage)

tie1=tme.time()
for i in urls:
    print i
    getsource(i)
print u'单线程时间' +str(time2-time1)


poo1=ThreadPool(5)
time3=time.time()
results=pool.mao(getsource,urls)
pool.close()
pool.join()
tiem4=time.time()
print '并行时间'+str(time4-time3)
```
