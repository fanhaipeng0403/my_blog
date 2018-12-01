---
title: Ubuntu(Debian)的aptitude与apt-get的区别和联系
date: 2016-05-04 12:20:33
tags: Linux

---
-----
域名解析
[_posts] nslookup                                      1:09:34  ☁  master ☂ ⚡ ✭
> www.baidu.com
Server:     127.0.1.1
Address:    127.0.1.1#53

Non-authoritative answer:
www.baidu.com   canonical name = www.a.shifen.com.
Name:   www.a.shifen.com
Address: 111.13.100.91
Name:   www.a.shifen.com
Address: 111.13.100.92

---------
wget --random-wait -r -p -e robots=off -U Mozilla www.baidu.com
递归下载整个网站

------
export PATH=$PATH:/usr/local/go/bin(把原来的PATH变量内容，添加上新的内容，然后在赋值个PATH)

export 是导出的意思，就父进程可以传给子进程的变量，即环境变量


----------
免去登录密码
首先在设置里的用户账号里设置，
然后取百度搜索去除密码环

搜索文件

find /home myfavourite1 | grep myfavourite

递归改变权限
chmod 777 × -R

echo sometext > somefile　覆盖
echo sometext >> somefile 追加

复制文件夹
cp -r ~/Downloads/resource .

管道符号是从左到右
想要从右到左可以使用

例如命令 Google cat data.json

grep 的使用，显示查找内容的上下文
标准unix/linux下的grep通过以下参数控制上下文

grep -C 5 foo file  显示file文件中匹配foo字串那行以及上下5行
grep -B 5 foo file  显示foo及前5行
grep -A 5 foo file  显示foo及后5行
查看grep版本的方法是

grep -V

按文件修改时间查看文件
ls -t
ls -rt

Linux中变量#,#,@,0,0,1,2,2,*,$$,$?的含义

$# 是传给脚本的参数个数
$0 是脚本本身的名字
$1 是传递给该shell脚本的第一个参数
$2 是传递给该shell脚本的第二个参数
$@ 是传给脚本的所有参数的列表
$ 是以一个单字符串显示所有向脚本传递的参数，与位置变量不同，参数可超过9个
$$ 是脚本运行的当前进程ID号
$? 是显示最后命令的退出状态，0表示没有错误，其他表示有错误
区别：@@

相同点：都是引用所有参数
不同点：只有在双引号中体现出来。假设在脚本运行时写了三个参数（分别存储在112 3）则”3）则”*” 等价于 “112 3”（传递了一个参数）；而“3”（传递了一个参数）；而“@” 等价于 “1””1””2” “$3”（传递了三个参数）

应用:

——-
#mkdir + cd
mkcd () {
    mkdir -p “$@”
        cd “$@”
}

——-
参考
http://www.cnblogs.com/kaituorensheng/p/4002697.html

----

bash函数有三种写法：

[plain] view plain copy print?
function func1 ()  {
    echo "This is an example of bash function 1"
}

function func2  {
    echo "This is an example of bash function 2"
}


func3 ()  {
    echo "This is an example of bash function 3"
}

但是，第一种写法在有的 bash版本下会报错。

----------
deb 安装
GDebi第三方工具
------------
