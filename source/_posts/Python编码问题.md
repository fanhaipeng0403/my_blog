---
title: Python编码问题
date: 2017-01-07 10:23:09
tags: Python

---

# Python3中encode和decode

## decode和encode概念

Python3的默认编码是UTF-8,encode('utf-8')特意把字符encode为UTF-8编码，出来的结果还是相同：b'\xe4\xb8\xad'。

![](http://s14.sinaimg.cn/mw690/0020jtpXzy6Sbx0ds3X9d)


**我的理解，encode的作用，使我们看到的直观的字符转换成计算机内的字节形式。decode刚好相反，把字节形式的字符转换成我们看的懂的、直观的、“人模人样”的形式。如下图。**

\x表示后面是十六进制，\xe4\xb8\xad即是二进制的11100100 10111000 10101101。也就是说汉字‘中’encode成字节形式，是11100100 10111000 10101101。同理，我们拿11100100 10111000 10101101也就是\xe4\xb8\xad来decode回来，就是汉字‘中’。完整的应该是b'\xe4\xb8\xad'，

**在Python3中，以字节形式表示的字符串则必须加上前缀b，也就是写成上文的b'xxxx'形式.**


-------

decode的作用是将其他编码的字符串转换成unicode编码，如str1.decode('gb2312')，表示将gb2312编码的字符串str1转换成unicode编码。在Python3中uicode字节码和真实字符表示在shell里等效。

encode的作用是将unicode编码转换成其他编码的字符串，如str2.encode('gb2312')，表示将unicode编码的字符串str2转换成gb2312编码。

------



## 字符的真实Unicode编码

字符在计算机的内存中统一是以Unicode编码的。只有在字符要被写进文件、存进硬盘或者从服务器发送至客户端（例如网页前端的代码）时会变成utf-8。
这些字符以Unicode的字节形式表现出来，露出它在内存中的庐山正面目的。这里有个照妖镜：

xxxx.encode/decode('unicode-escape')

![](http://s7.sinaimg.cn/mw690/0020jtpXzy6SbxebbT0a6)

-------
- b'\\u4e2d'还是b'\u4e2d，一个斜杠貌似没影响

- 直接输'\u4e2d'和输入b'\u4e2d'.decode('unicode-escape')是相同的，都会打印出汉字‘中’，就是说你要是在shell里输入一个字符的UIcode的16进制字节串形式，会自动输出它对于的字符。也就是说，‘\uxxxx’格式的Unicode字符可被辨识且被等价于str类型。
-------


## 字符编码的转换(默认转为UTF-8)


**怎么变成UTF-8的字节码呢。懂了以上这些，现在我们就有思路了，先decode(要知道字节串的编码方式）变为真实世界的可视字符，再encode(要指定编码，不指定默认是解释器的默认编码）。**

```
xx.decode('unicode-escape').encode()
```

## unicode 和 utf-8的区别

```
In [1]: bin(0xe4b8ad)
Out[1]: ‘0b1110**0100**10**111000**10**101101**’

In [2]: bin(0x4e2d)
Out[2]: '0b100111000101101
```

unicode是全体字符和数字的一个映射关系,比如’A’是65,’中’是20013.
每个字符用的字节数以那个用了最大字节数的字符来确定,其他补充为0.
如果以这个映射关系进行储存传输,无疑会很浪费资源.

UTF-8的编码规则很简单，只有二条：

1）对于单字节的符号，字节的第一位设为0，后面7位为这个符号的unicode码。因此对于英语字母，UTF-8编码和ASCII码是相同的。

2）对于n字节的符号（n>1），第一个字节的前n位都设为1，第n+1位设为0，后面字节的前两位一律设为10。剩下的没有提及的二进制位，全部为这个符号的unicode码。




```
In [1]: hex(ord('中'))
Out[1]: '0x4e2d'

In [2]: '\u4e2d'
Out[2]: '中'

In [3]: '中'.encode('utf-8')
Out[3]: b'\xe4\xb8\xad'

In [4]: '中'.encode('unicode-escape')
Out[4]: b'\\u4e2d'

n [5]: b'\u4e2d'.decode('unicode-escape')
Out[5]: '中'

In [6]: b'\xe4\xb8\xad'.decode('utf-8')
Out[6]: '中

b'\xe4\xb8\xad' ,b'\\u4e2d'

```



.
