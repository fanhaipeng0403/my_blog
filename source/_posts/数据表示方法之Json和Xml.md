---
title: 数据表示方法之Json和Xml
date: 2016-06-26 22:33:55
tags: Python

---
Web Service的行业发展趋势是从XML转向JSON。由于JSON足够简单，能够直接映射到编程语言已有的原生数据结构，JSON的使用让解析与数据抽取变得更简单。但是，XML比JSON在自我描述方面更强，因此在某些应用程序中XML仍然有一定优势。

## XML节点循环

```
import xml.etree.ElementTree as ET
input = "'
<stuff>
    <users>
        <user x="2">
            <id>001</id>
            <name>Chuck</name>
        </user>
        <user x="7">
            <id>009</id>
            <name>Brent</name>
        </user>
    </users>
</stuff>"'
stuff = ET.fromstring(input)
lst = stuff.findall('users/user')
print 'User count:', len(lst)
for item in lst:
    print 'Name', item.find('name').text
    print 'Id', item.find('id').text
    print 'Attribute', item.get('x')
```
<!--more-->

-----------
User count: 2
Name Chuck
Id 001
Attribute 2
Name Brent
Id 009
Attribute 7

## Json节点循环
```
import json
input = "'
[
  { "id" : "001",
    "x" : "2",
    "name" : "Chuck"
  } ,
  { "id" : "009",
    "x" : "7",
    "name" : "Brent"
  }
]"'
info = json.loads(input)
print 'User count:', len(info)
for item in info:
    print 'Name', item['name']
    print 'Id', item['id']
    print 'Attribute', item['x']
    User count: 2
```
--------
Name Chuck
Id 001
Attribute 2
Name Brent
Id 009
Attribute 7

JSON经过解析后，我们就得到了原生的Python对象与结构。由于返回的数据就是简单的原生Python结构，就没必要使用JSON库继续深入解析JSON了。
