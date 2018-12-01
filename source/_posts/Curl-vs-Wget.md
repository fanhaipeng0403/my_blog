---
title: Curl vs Wget
date: 2017-02-04 09:43:05
tags:  Linux
---


共性

都是可以从FTP、HTTP、HTTPS下载内容的命令行工具
都可以发送HTTP POST请求
都支持HTTP cookies
都被设计为工作中无需用户干涉——像内置脚本一样
都是完全开源免费的
都是90年代的项目
都支持metalink


差异

curl：

库。curl由libcurl——一个API稳定且使用自由的跨平台库技术支持。这个主要的差别使二者产生了完全不同的内部体系。当然制作库也是比一个“单纯的”命令行工具要稍微难一点的。
管道。curl工作起来更像是传统unix的cat命令，基于“万事无不管道”的态度它向stdout发送更多信息，从stdin读取更多。Wget类比起来则更像cp命令。
单次性。curl本质上是做单次数据转移的。它只转移用户指定的URLs，并不包括任何递归的下载逻辑或是各种HTML的解析器。
更多的协议。curl支持FTP、FTPS、Gopher、HTTP、HTTPS、SCP、SFTP、TFTP、TELNET、DICT、LDAP、LDAPS、FILE、POP3、IMAP、SMB/CIFS、SMTP、RTMP和RTSP。Wget仅支持HTTP、HTTPS和FTP。
更轻便。相比wget，curl可构建和运行在更多平台上。举个栗子：OS/400，TPS和其他非直系unix拷贝的“外来”平台。
更多的SSL库和SSL支持。curl可以用11种(11种！)不同的SSL/TLS库来构建，并且为协议细节提供了更多控制权和尽可能的支持。
HTTP认证。curl支持更多HTTP认证的方法，尤其是HTTP代理：Basic、Digest、NTLM和Negotiate。
SOCKS。curl支持好几个版本SOCKS协议的代理访问。
双向性。curl可以提供上传和发送的能力。Wget只能提供简单的HTTP POST支持。
HTTP多部分/格式数据的发送，这允许用户在一般的模拟浏览器中进行HTTP“上传”以及进行HTTP自动化来扩展内容。
curl支持gzip以及压缩内容编码，并且会自动解压。
curl提供并且压缩传输编码的HTTP，wget则不。
curl支持HTTP/2并且使用Happy Eyeballs[1]进行双栈连接。
更活跃的开发者。这可能会引发讨论，我基于如下三点考虑：邮件列表活跃度、源代码提交频次以及发布频次。任何跟进这两个项目的人都可以注意到curl在这三点均有着更高的数据，并且已经保持了10年以上。在openhub上比较
Wget

Wget仅仅是命令行工具而非库。
递归性！Wget相对于curl而言主要的强势之处在于它可以递归下载，或是下载在远程资源中提到的任何资源，无论是一个HTML页面还是一个FTP目录列表。
更老的资历。Wget可以追溯的1995年，而curl不会早于1996年末。
GPL。Wget是GPL第三版协议。curl是MIT许可。
GNU。Wget是GNU计划的一部分，版权指定为FSF。curl项目则完全独立并且脱离于任何父级组织，几乎所有版权被Daniel所有。
Wget不需要额外的指令选项去下载远程的URL至本地文件，curl需要 -o或者 -O。
Wget的SSL/TLS支持仅有GnuTLS或者OpenSSL。
Wget仅支持Basic认证作为唯一的HTTP代理。
Wget没有SOCKS支持。
可以从提前中断的传输中回复并且继续下载，curl则没有对应的功能。
Wget默认开启更多设置：cookies、重定向跟随、远程资源的时间戳等。curl的大多数这些设置需要单独开启。
Wget四个字母在传统键盘上仅用左手就能输入！

转于 http://www.cnblogs.com/mangi/p/5584838.html
