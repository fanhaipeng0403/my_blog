---
title: API集成
date: 2016-07-04 09:45:11
tags: Web
categories: Python

---

# 使用 requests 访问 Web APIs

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import urllib2

gh_url = 'https://api.github.com'

req = urllib2.Request(gh_url)

password_manager = urllib2.HTTPPasswordMgrWithDefaultRealm()
password_manager.add_password(None, gh_url, 'user', 'pass')

auth_manager = urllib2.HTTPBasicAuthHandler(password_manager)
opener = urllib2.build_opener(auth_manager)

urllib2.install_opener(opener)

handler = urllib2.urlopen(req)

print handler.getcode()
print handler.headers.getheader('content-type')

# ------
# 200
# 'application/json'
```

```
#!/usr/bin/env python
# -*- coding: utf-8 -*-

import requests

r = requests.get('https://api.github.com', auth=('user', 'pass'))

print r.status_code
print r.headers['content-type']

# ------
# 200
# 'application/json'
```

显而易见，用requests模块更省事。


```
u'[{"created_at":"2014-06-08T20:50:27-07:00","payload":{"sha...
Requests will automatically decode content from the server. The text encoding guessed by Requests is used when you access r.text. You can find out what encoding Requests is using, and change it, using the r.encoding property:

'utf-8'
There's an builtin JSON decoder on which we heavily rely on

[{u'actor_attributes': {u'name': u'Tin...

payload = {'key1': 'value1', 'key2': 'value2'}
You can see that the URL has been correctly encoded by printing the URL:

http://httpbin.org/get?key2=value2&key1=value1
```

你也可以自定义你的Headers

 
```
 r = requests.get('http://httpbin.org/get')
200

404

Traceback (most recent call last):
File "requests/models.py", line 832, in raise_for_status
    raise http_error
requests.exceptions.HTTPError: 404 Client Error
Response.raise_for_status() returns None for status_code 200
```


```
r.headers
{
    'content-encoding': 'gzip',
    'transfer-encoding': 'chunked',
    'connection': 'close',
    'server': 'nginx/1.0.4',
    'x-runtime': '148ms',
    'etag': '"e1ca502697e5c9317743dc078f67693f"',
    'content-type': 'application/json'
}

'application/json'
```



```
requests.get('http://github.com', timeout=0.001)
Traceback (most recent call last):
requests.exceptions.Timeout: Request timed out.
```


```
n [3]: url = 'https://api.github.com/users/sayanchowdhury/repos?page=1&per_page
   ...: =10'
   ...: r = requests.head(url=url)
   ...: 

In [4]: 

In [4]: r.links
Out[4]: 
{'last': {'rel': 'last',
  'url': 'https://api.github.com/user/500628/repos?page=11&per_page=10'},
 'next': {'rel': 'next',
  'url': 'https://api.github.com/user/500628/repos?page=2&per_page=10'}}
```


http://docs.python-requests.org/zh_CN/latest/user/quickstart.html


