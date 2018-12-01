---
title: Css性能优化
date: 2017-01-01 11:49:24
tags: FrontEnd
categories: FrontEnd

---
# 优化原因

和电脑软件不同，网页应用并不需要一个独立的安装过程，它只需要输入RUL地址，然后我们就可以开始运行应用了——这就是网络应用的一个关键特性。
然而要想获得这种瞬间达成的效果，我们非得先获取那些加起来足有几MB的数据，然后在几百毫秒内，把这几十上百份资源集合起来才行

# 优化目的

让内容更快的呈现在用户面前。

# 优化手段

## 衡量每份资源的价值


价值和开销要成正比，没有用的，直接删掉。

## 预处理
```
<html>
      <head>
      <style>
         /* awesome-container is only used on the landing page */
         .awesome-container { font-size: 120% }
         .awesome-container { width: 50% }
      </style>
     </head>
    
     <body>
       <!-- awesome container content: START -->
        <div>…</div>
       <!-- awesome container content: END -->
       <script>
         awesomeAnalytics(); // beacon conversion metrics
       </script>
     </body>
    </html>
```

去除重复的Css选择器，去除无用的注释，去除制表符，处理后

```
 <html><head><style>.awesome-container{font-size:120%;width: 50%}
    </style></head><body><div>…</div><script>awesomeAnalytics();
    </script></body></html>
```


## 压缩

服务器配置压缩手段，压缩可被压缩的内容，减小传输体积，缩短时间。

配置参考:https://github.com/h5bp/server-configs

## 缓存

**基本原理**

------
- HTTP发出请求后，会先去浏览器缓存，检查是否有有效缓存响应，有了，直接响应，没有，再请求服务器。

#### [Cache-Control](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)

#### Cache-Control参数

no-store,禁止缓存对响应进行复制。

no-cache,以前老认为这个是不缓存的意思，下面从《HTTP权威指南》摘录一段解释：标识为 no-cache 的响应实际上是可以存储在本地缓存区中的。 只是在与原始服务器进行新鲜度再验证之前，缓存不能将其提供给客户端使用。这个首部使用 donot-serve-from-cache-without-revalidation 这个名字会更恰当一些。

must-revalidate,在事先没有跟原始服务器进行再验证的情况下，不能提供这个对象的陈旧副本。 缓存仍然可以随意提供新鲜的副本。如果在缓存进行 must-revalidate 新鲜度检查时，原始服务器不可用，缓存就必须返回一条 504 Gateway Timeout 错误。

max-age=3600,从服务器将文档传来之时起， 可以认为此文档处于新鲜状态的秒数。


### 接收缓存控制头
![](http://wf.uisdc.com/cn/performance/optimizing-content-efficiency/images/http-request.png)

初次请求，服务器返回了一个1024字节的响应，指示客户端缓存120秒，并提供了一个验证令牌（“x234dff”），这个令牌，可以在浏览器中的响应过期后，检查服务器的资源是否更新过。


#### 强缓存,Max-age

当资源的缓存还在有效期时，浏览器直接从本地缓存中取资源。


#### 协商缓存,Etag

  ![](http://wf.uisdc.com/cn/performance/optimizing-content-efficiency/images/http-cache-control.png)
在HTTP请求头中，提供了ETag令牌，服务器针对当前资源检查令牌，如果没有发生更改，则返回“304 Not Modified（304未更改）”响应，以告知浏览器它缓存中所存有的这个响应还可以用，并可以再延长120秒。


![](https://dn-cnode.qbox.me/FjK1Jxu_BS-eYytLgoKJqdXUHcQm)

![](http://wf.uisdc.com/cn/performance/optimizing-content-efficiency/images/http-cache-decision-tree.png)

## 图片优化

http://wf.uisdc.com/cn/performance/optimizing-content-efficiency/image-optimization.html#section-1
## 内容选择
http://wf.uisdc.com/cn/performance/critical-rendering-path/#optimize-images-for-performance
参考
     http://wf.uisdc.com/cn/performance/optimizing-content-efficiency/images/http-cache-decision-tree.png
     https://www.zhihu.com/question/20790576
     http://wf.uisdc.com/cn/performance/optimizing-content-efficiency/http-caching.html
