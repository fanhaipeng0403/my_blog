---
title: WEB设计模式
date: 2016-08-03 22:24:59
tags:
categories: Others

---

推荐 https://zhuanlan.zhihu.com/p/22834622

# 前言

在想弄懂这些名词的过程中，看了很多文章，觉得在将MVC时，应该先注意到：

```
今天无数经过演绎的MVC实现（如backbone）和科普文，要么是原本作者概念已经很混乱，掺杂私货，要么为了适配现代的标记语言和控件模式，自己修改了经典MVC中的一些概念和耦合关系。实际上今天MVC已经没法作为一种交流的标准词汇了。`
```

```
MVC在bs架构和cs架构上差别很大，即使同是bs，因为使用的技术的差别，业务的差别，架构的差别，MVC的通信方式也会和原来你书本上看到的不一样。就像backbonejs和angularjs的出现，是发明还是延伸，还是糟蹋？每天和它一起工作的人才知道。
所有的设计应该以贴近自然或接近自然规律为目标。再通俗的讲，用的舒服就是自然。好的东西绝对不需要强记一堆原理来理解的。
```

个人觉得，MVC是更多的是在一种思想上去理解。而不是一种标准。


##  MVC和MVVC图解
![](https://camo.githubusercontent.com/2a09625439c430f360a770c80702f8df2c996156/687474703a2f2f7777332e73696e61696d672e636e2f6d773639302f34373465626633357477316476716e77786338746b6a2e6a7067?_=4285171)

##  REST

自从Roy Fielding博士在2000年他的博士论文中提出REST（Representational State Transfer）风格的软件架构模式后，REST就基本上迅速取代了复杂而笨重的SOAP，成为Web API的标准了。

什么是Web API呢？

如果我们想要获取某个电商网站的某个商品，输入http://localhost:3000/products/123，就可以看到id为123的商品页面，但这个结果是HTML页面，它同时混合包含了Product的数据和Product的展示两个部分。对于用户来说，阅读起来没有问题，但是，如果机器读取，就很难从HTML中解析出Product的数据。

如果一个URL返回的不是HTML，而是机器能直接解析的数据，这个URL就可以看成是一个Web API。比如，读取http://localhost:3000/api/products/123，如果能直接返回Product的数据，那么机器就可以直接读取。
REST就是一种设计API的模式。最常用的数据格式是JSON。由于JSON能直接被JavaScript读取，所以，以JSON格式编写的REST风格的API具有简单、易读、易用的特点。

编写API有什么好处呢？由于API就是把Web App的功能全部封装了，所以，通过API操作数据，可以极大地把前端和后端的代码隔离，使得后端代码易于测试，前端代码编写更简单。

此外，如果我们把前端页面看作是一种用于展示的客户端，那么API就是为客户端提供数据、操作数据的接口。这种设计可以获得极高的扩展性。例如，当用户需要在手机上购买商品时，只需要开发针对iOS和Android的两个客户端，通过客户端访问API，就可以完成通过浏览器页面提供的功能，而后端代码基本无需改动。

当一个Web应用以API的形式对外提供功能时，整个应用的结构就扩展为：

![](http://www.liaoxuefeng.com/files/attachments/001473591163887539f974f19544a10a1e89b8cf9f46048000/l)

##  REST精要

REST

a，出身：由Roy Thomas Fielding博士于2000年提出


b，全称：Representational state Transfer,称为表象化状态转变，或者表述性状态转移

c，REST是Web服务的一种架构风格

d，使用HTTP、URI等广泛流行的标准和协议

e，轻量级、跨平台、跨语言的架构设计

那么，从上面5点总结来看，REST到底是个什么鬼呢？好了，下面要注意了，重点来了：**REST是一种设计风格，它既不是一种标准，也不是一种软件，而是一种思想。它通常使用HTTP、URI和XML、json以及HTML这些现有的流行的协议和标准**

## REST架构的主要原则

a，网络上的所有资源都可以被抽象为资源（Resource）

b，每个资源都有一个唯一的资源标识符（Resource identifier）

c，同一资源具有多种表现形式，例如xml，json

d，对资源的各种操作不会改变资源的标识符

e，所有的操作都是无状态的（stateless）[无状态：HTTP是无状态协议。无状态是指协议对于事务处理没有记忆能力，如果后续需要前面的信息，则它必须重传，这样可能导致每次连接传送的数据量增大]

f，符合REST原则的架构方式均可被称为RESTful

## REST对资源的操作


-GET：表示获取一个资源

-POST：表示创建一个新的资源

-PUT：表示修改一个资源的状态

-DELETE：表示删除一个资源

资源展现：-XML    -JSON

## RESTful

a，RESTful对应中文是REST式的

b，RESTful WebService 是一种常见的REST的应用，是遵守REST风格以及Web风格的Web服务

c，REST式的Web服务是一种ROA（(Resource-Oriented Architecture，面向资源架构）


```
虽然REST开发方式很好，但直到现在为止，MVC(Model-View-Controller) 模式依然是Web开发最普遍的模式，绝大多数的公司和开发人员都采取此种架构来开发Web应用，并且其思维方式也停留于此。MVC模式由数据，视图和控制 器构成，通过事件(Event)触发Controller来改变Model和View。加上Webwork,Struts等开源框架的加入，MVC开发模 式已经相当成熟，其思想根本就是基于Action来驱动。从开发人员角度上来说，贸然接受一个新的架构会带来风险，其中的不确定因素太多。并且REST新 的思维方式是把所有用户需求抽象为资源，这在实际开发中是比较难做到的，因为并不是所有的用户需求都能被抽象为资源，这样也就是说不是整个系统的结构都能 通过REST的来表现。所以在开发中，我们需要根据以上2点来在REST和MVC中做出选择。我们认为比较好的办法是混用REST和MVC，因为这适合绝 大多数的Web应用开发，开发人员只需要对比较容易能够抽象为资源的用户需求采取REST的开发模式，而对其它需求采取MVC开发即可。这里需要提到的就 是ROR(Ruby on Rails)框架，这是一个基于Ruby语言的越来越流行的Web开发框架，它极大的提高了Web开发的速度。更为重要的是，ROR(从1.2版本起)框 架是第一个引入REST做为核心思想的Web开发框架，它提供了对REST最好的支持，也是当今最成功的应用REST的Web开发框架。实际上，ROR的 REST实现就是REST和MVC混用，开发人员采用ROR框架，可以更快更好的构建Web应用。
```

个人理解，MCV是从过程解决问题的一种思维，RESRFUL是一种从资源对象方面解决的问题的思维

个人理解，MCV是从过程解决问题的一种思维，RESRFUL是一种从资源对象方面解决的问题的思维。

# Webhook

        webhook（也被称为网络回调或HTTP推送API）被视为一个应用为其他应用提供实时信息的一种方法。当webhook被触发后，它将传送数据到其他应用程序中去，这就意味着你会立即获取到数据。
        webhook通过一台服务器的工作，在有事发生时，发送到特定的URL数据，到另一台服务器。
        就像一个钩子一样连接着其他程序。

        ![](https://segmentfault.com/img/remote/1460000006971575?w=550&h=400)

## webhooks模式的主要优点

        无需周期性地调用APIs。相反，当一些有趣的事情发生之后，APIs将通过特定端点通知的方式来访问你的应用。现在缺少的是一种以编程方式告诉APIs你所感兴趣的接收呼叫和注册端点。

        这里有一个常见的例子：你到github上。有一个用于他们代码POST请求webhook的文本框。你输入一个URL。现在当你上传你的代码到github上时，github将会通过HTTP POST的方法请求你所选择的包含详细信息的URL。没有更简单的方法以便与任意Web服务进行开放式集成


        http://jnn.iteye.com/blog/83095
http://www.cnblogs.com/hoojo/p/longPolling_comet_jquery_iframe_ajax.html
http://stackoverflow.com/questions/23172760/differences-between-webhook-and-websocket


WebSocket

WebSocket是HTML5新增的协议，它的目的是在浏览器和服务器之间建立一个不受限的双向通信的通道，比如说，服务器可以在任意时刻发送消息给浏览器。

为什么传统的HTTP协议不能做到WebSocket实现的功能？这是因为HTTP协议是一个请求－响应协议，请求必须先由浏览器发给服务器，服务器才能响应这个请求，再把数据发送给浏览器。换句话说，浏览器不主动请求，服务器是没法主动发数据给浏览器的。

这样一来，要在浏览器中搞一个实时聊天，在线炒股（不鼓励），或者在线多人游戏的话就没法实现了，只能借助Flash这些插件。

也有人说，HTTP协议其实也能实现啊，比如用轮询或者Comet。轮询是指浏览器通过JavaScript启动一个定时器，然后以固定的间隔给服务器发请求，询问服务器有没有新消息。这个机制的缺点一是实时性不够，二是频繁的请求会给服务器带来极大的压力。

Comet本质上也是轮询，但是在没有消息的情况下，服务器先拖一段时间，等到有消息了再回复。这个机制暂时地解决了实时性问题，但是它带来了新的问题：以多线程模式运行的服务器会让大部分线程大部分时间都处于挂起状态，极大地浪费服务器资源。另外，一个HTTP连接在长时间没有数据传输的情况下，链路上的任何一个网关都可能关闭这个连接，而网关是我们不可控的，这就要求Comet连接必须定期发一些ping数据表示连接“正常工作”。

以上两种机制都治标不治本，所以，HTML5推出了WebSocket标准，让浏览器和服务器之间可以建立无限制的全双工通信，任何一方都可以主动发消息给对方。

WebSocket协议

WebSocket并不是全新的协议，而是利用了HTTP协议来建立连接。我们来看看WebSocket连接是如何创建的。

首先，WebSocket连接必须由浏览器发起，因为请求协议是一个标准的HTTP请求，格式如下：

GET ws://localhost:3000/ws/chat HTTP/1.1
Host: localhost
Upgrade: websocket
Connection: Upgrade
Origin: http://localhost:3000
Sec-WebSocket-Key: client-random-string
Sec-WebSocket-Version: 13
该请求和普通的HTTP请求有几点不同：

GET请求的地址不是类似/path/，而是以ws://开头的地址；
请求头Upgrade: websocket和Connection: Upgrade表示这个连接将要被转换为WebSocket连接；
Sec-WebSocket-Key是用于标识这个连接，并非用于加密数据；
Sec-WebSocket-Version指定了WebSocket的协议版本。
随后，服务器如果接受该请求，就会返回如下响应：

HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: server-random-string
该响应代码101表示本次连接的HTTP协议即将被更改，更改后的协议就是Upgrade: websocket指定的WebSocket协议。

版本号和子协议规定了双方能理解的数据格式，以及是否支持压缩等等。如果仅使用WebSocket的API，就不需要关心这些。

现在，一个WebSocket连接就建立成功，浏览器和服务器就可以随时主动发送消息给对方。消息有两种，一种是文本，一种是二进制数据。通常，我们可以发送JSON格式的文本，这样，在浏览器处理起来就十分容易。

为什么WebSocket连接可以实现全双工通信而HTTP连接不行呢？实际上HTTP协议是建立在TCP协议之上的，TCP协议本身就实现了全双工通信，但是HTTP协议的请求－应答机制限制了全双工通信。WebSocket连接建立以后，其实只是简单规定了一下：接下来，咱们通信就不使用HTTP协议了，直接互相发数据吧。

安全的WebSocket连接机制和HTTPS类似。首先，浏览器用wss://xxx创建WebSocket连接时，会先通过HTTPS创建安全的连接，然后，该HTTPS连接升级为WebSocket连接，底层通信走的仍然是安全的SSL/TLS协议。

浏览器
很显然，要支持WebSocket通信，浏览器得支持这个协议，这样才能发出ws://xxx的请求。目前，支持WebSocket的主流浏览器如下：

Chrome
Firefox
IE >= 10
Sarafi >= 6
Android >= 4.4
iOS >= 8
服务器

由于WebSocket是一个协议，服务器具体怎么实现，取决于所用编程语言和框架本身。Node.js本身支持的协议包括TCP协议和HTTP协议，要支持WebSocket协议，需要对Node.js提供的HTTPServer做额外的开发。已经有若干基于Node.js的稳定可靠的WebSocket实现，我们直接用npm安装使用即可。

目前要实现消息实时推送，有两种方法，一种是ajax轮询，由客户端不停地请求服务器端，查询有没有新消息，然后再由服务器返回结果；另外一种就是long poll,通过一次请求，询问服务器有没有新消息更新，如果没有新消息时，会保持长连接，就一直不返回Response给客户端。直到有消息才返回，返回完之后，客户端再次建立连接，周而复始。这两种都是单向链接，需要被动的请求服务器，而不是由服务器自动发给客户端。

从上面可以看出其实这两种方式，都是在不断地建立HTTP连接，然后等待服务端处理，可以体现HTTP协议的另外一个特点，被动性。
何为被动性呢，其实就是，服务端不能主动联系客户端，只能有客户端发起。
简单地说就是，服务器是一个很懒的冰箱（这是个梗）（不会、不能主动发起连接），但是上司有命令，如果有客户来，不管多么累都要好好接待。


webSocket文章:

https://www.zhihu.com/question/20215561
http://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001472780997905c8f293615c5a42eab058b6dc29936a5c000
