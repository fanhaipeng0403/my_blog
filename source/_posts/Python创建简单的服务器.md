---
title: node.js或Python创建简单的服务器
date: 2017-01-13 22:22:01
tags:
categories: Python

---

# Node.js临时服务器(推荐)

```
sudo npm install anywhere -g
```

# Python临时服务器

使用Python创建简单的HTTP和FTP服务

python -m SimpleHTTPServer 80
后面的80端口是可选的，不填会采用缺省端口8000。注意，这会将当前所在的文件夹设置为默认的Web目录，试着在浏览器敲入本机地址：

http://localhost:80
如果当前文件夹有index.html文件，会默认显示该文件，否则，会以文件列表的形式显示目录下所有文件。这样已经实现了最基本的文件分享的目的，你可以做成一个脚本，再建立一个快捷方式，就可以很方便的启动文件分享了。如果有更多需求，完全可以根据自己需要定制，具体的请参见官方文档SimpleHTTPServer，或者直接看源码。我拷贝一段，方便参考：


```
import SimpleHTTPServer
import SocketServer

PORT = 8000

Handler = SimpleHTTPServer.SimpleHTTPRequestHandler

httpd = SocketServer.TCPServer(("", PORT), Handler)

    print "serving at port", PORT
httpd.serve_forever()
    ```

    Python版FTP服务器

    看到这里，默认你已经安装了Python，不过你还需要安装另外一个好用的工具。你知道，当需要找Chrome插件的时候，会去Google的WebStore；当需要找Firefox应用的时候，会去Mozilla的Add-ons；当你需要找Python组件的时候，你需要pip:A tool for installing and managing Python packages，安装方法就不介绍了。

    Python没有内置一个直接可以用的FTP服务器，所以需要第三方组件的支持，我找到的这个组件叫pyftpdlib，首先安装：

    pip install pyftpdlib
    安装完后，和HTTP服器类似，执行以下命令就可以启动一个FTP服务器了：

    python -m pyftpdlib -p 21
    后面的21端口依然是可选的，不填会随机一个，被占用的端口将跳过。在浏览器敲入本机地址：

    ftp://localhost:21
    这时候，是匿名访问，也就是用户名是anonymous，密码为空，如果想要控制访问权限，你需要自己定制服务器，具体的可以参看pyftpdlib Tutorial，我这里拷贝过来一段作为介绍：


    ```
    from pyftpdlib.authorizers import DummyAuthorizer
    from pyftpdlib.handlers import FTPHandler
    from pyftpdlib.servers import FTPServer

    def main():
# Instantiate a dummy authorizer for managing 'virtual' users
        authorizer = DummyAuthorizer()

# Define a new user having full r/w permissions and a read-only
# anonymous user
    authorizer.add_user('user', '12345', '.', perm='elradfmwM')
authorizer.add_anonymous(os.getcwd())

# Instantiate FTP handler class
    handler = FTPHandler
    handler.authorizer = authorizer

# Define a customized banner (string returned when client connects)
    handler.banner = "pyftpdlib based ftpd ready."

# Specify a masquerade address and the range of ports to use for
# passive connections.  Decomment in case you're behind a NAT.
#handler.masquerade_address = '151.25.42.11'
#handler.passive_ports = range(60000, 65535)

# Instantiate FTP server class and listen on 0.0.0.0:2121
    address = ('', 2121)
server = FTPServer(address, handler)

# set a limit for connections
    server.max_cons = 256
    server.max_cons_per_ip = 5

# start ftp server
server.serve_forever()

    if __name__ == '__main__':
main()
    ```

    只看代码应该基本知道该怎么用了，add_user显然是添加用户，2121是指定端口，当然也可以随机，还有最大连接数max_cons，每个ip最大连接限制，更多的接口建议直接看docstrings。

    后记

    Python第三方组件就是个大宝库，基本上我自己遇到的大部分问题都可以在这里面找到解决文案。同时，建议喜欢折腾的程序员，甚至没有程序背景的IT人员，都尝试学习一下这门语言，这对解决问题的能力以及思维的锻炼都有莫大裨益。


# 在终端生产二维码

    npm install -g qrcode-terminal

    http://www.cnblogs.com/yili16438/p/d3209323913c6d53e6060fcd8d27e4c0.html
