---
title: Mysql
date: 2017-01-21 11:16:11
tags: Mysql

---

# 介绍

MySQL可为你提供3类有价值的信息：

查询结果信息 受SELECT、UPDATE 或 DELETE 语句影响的记录数量。
表与数据库的信息 表及数据库的相关信息。
MySQL 服务器的信息 数据库服务器的状态以及数据库版本号等信息。


# Python与mysql

使用pymysql 或者 mysqldb(只能用于python2)

http://www.jb51.net/article/92516.htm



# 安装

```
1.sudo apt-get install mysql-server

2.apt-get isntall mysql-client

3.sudo apt-get install libmysqlclient-dev

4. sudo apt-get install libmysqld-dev (原来使用apt-get安装的MySQL是没有mysql_config这个文件的,不然安装pip install mysql-python会报错)

检查安装上了没

sudo netstat -tap | grep mysq
mysql --version

```

# 彻底卸载

```
sudo apt-get remove mysql-server
sudo apt-get autoremove mysql-server
sudo apt-get remove mysql-common
dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P

卸载完后看看mysql命令还能用么,如果还有,强制删除:
rm -rf /usr/bin/mysql

```

# 登录


mysql　-D　所选择的数据库名 -h 主机名 -u 用户名 -p

用createtable.sql内的语句,在samp_db创建一个表
mysql -D samp_db -u root -p < createtable.sql



# 关闭,启动和重启

关闭情况下使用mysql会报错

```
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
```

检查是否运行了

```
ps -ef | grep mysqld
```


------

以Service方式启动/停止/重启MySQL命令：


```
service mysql start

service mysql stop

service mysql restart

另外一些发行版本会重命名为mysqld

service mysqld start

service mysqld stop

service mysqld restart

```

-------
service 命令就是调用/etc/init.d/下边的脚本来启动服务,可以直接这么操作

```
/etc/init.d/mysqld start

/etc/init.d/mysqld stop

/etc/init.d/mysqld restart
```


# 命令

### 哪些库

show databases;

### 选择库

use XXXX;

### 库有哪些表

show tables;
show tables from xxx


### 表的列信息

show columns from XXX;
show columns from mysql.user;


### 表创建时的信息

SHOW CREATE TABLE `user` \G
这样可以看到创建时信息,可以克隆一张表

http://wiki.jikexueyuan.com/project/mysql/clone-tables.html

### 表的引擎，版本，名称等信息

http://m.studyofnet.com/news/1299.html

某个库所有的表
show table status from db_name

指定库内的某个表
show table status from db_name like 'user'\G;

### 表的索引信息

索引（Index）：它在数据库中的作用就像书后的索引一样,是为了加快搜索。

show index from xxx

http://database.51cto.com/art/201005/201345.htm

### 创建库

create database 数据库名 [其他选项];
create database samp_db character set gbk;
创建samp_dab,它的编码是gbk

或者

mysqladmin -u root -p create TUTORIALS
mysqladmin -u root -p drop TUTORIALS

### 创建表


## 操作

### 增

insert [into] 表名 [(列名1, 列名2, 列名3, ...)] values (值1, 值2, 值3, ...);

insert into students (name, sex, age) values("孙丽华", "女", 21);

### 删

删除 id 为 2 的行: delete from students where id=2;

删除所有年龄小于 21 岁的数据: delete from students where age<20;

删除表中的所有数据: delete from students;

### 改

update 表名称 set 列名称=新值 where 更新条件

将 id 为 5 的手机号改为默认的"-":
update students set tel=default where id=5;

将所有人的年龄增加 1:
update students set age=age+1;

将手机号为 13288097888 的姓名改为 "张伟鹏", 年龄改为 19:
update students set name="张伟鹏", age=19 where tel="13288097888";


### 查

以查询所有性别为女的信息为例, 输入查询语句: select * from students where sex="女";

where 子句不仅仅支持 "where 列名 = 值" 这种名等于值的查询形式, 对一般的比较运算的运算符都是支持的, 例如 =、>、<、>=、<、!= 以及一些扩展运算符 is [not] null、in、like 等等。 还可以对查询条件使用 or 和 and 进行组合查询, 以后还会学到更加高级的条件查询方式, 这里不再多做介绍。


示例:

查询年龄在 21 岁以上的所有人信息: select * from students where age > 21;

查询名字中带有 "王" 字的所有人信息: select * from students where name like "%王%";

查询 id 小于 5 且年龄大于 20 的所有人信息: select * from students where id<5 and age>20;

更新表中的数据

select 列名称 from 表名称 where 条件;

用or代替in

SELECT * FROM employee_tbl WHERE daily_typing_pages IN ( 250, 220, 170 );


## 创建后表的修改

```
alter table 语句用于创建后对表的修改, 基础用法如下:

添加列
基本形式: alter table 表名 add 列名 列数据类型 [after 插入位置];

示例:

在表的最后追加列 address: alter table students add address char(60);

在名为 age 的列后插入列 birthday: alter table students add birthday date after age;

修改列
基本形式: alter table 表名 change 列名称 列新名称 新数据类型;

示例:

将表 tel 列改名为 telphone: alter table students change tel telphone char(13) default "-";

将 name 列的数据类型改为 char(16): alter table students change name name char(16) not null;

删除列
基本形式: alter table 表名 drop 列名称;

示例:

删除 birthday 列: alter table students drop birthday;

重命名表
基本形式: alter table 表名 rename 新表名;

示例:

重命名 students 表为 workmates: alter table students rename workmates;

删除整张表
基本形式: drop table 表名;

示例: 删除 workmates 表: drop table workmates;

删除整个数据库
基本形式: drop database 数据库名;

示例: 删除 samp_db 数据库: drop database samp_db;
```



# 用户管理

http://www.cnblogs.com/jevo/p/3257228.html

## 新建用户

grant select,insert,update,delete
on mydb.*
to test1@localhost
identified by "123456"
`

# 脚手架

```
pip install mycli
```
http://www.wtoutiao.com/p/m94kjr.html

mycli -u root

直接输入mycli默认连接的当前shell用户

```



# 获取服务器元数据

利用下面5种命令可以获取数据库服务器上的各种关键信息。它们既适用于命令行，也适用于 PHP 或 PERL 脚本。

命令	描述
SELECT VERSION()	表明服务器版本的字符串
SELECT DATABASE()	当前数据库名称（如果没有则为空值）
SELECT USER()	当前用户名
SHOW STATUS	服务器状态指示器
SHOW VARIABLES	服务器配置变量


# mysqlworkbench

下载
http://jingyan.baidu.com/article/c843ea0b81786d77931e4a95.html
教程
http://jingyan.baidu.com/article/c843ea0b81786d77931e4a95.html

MySQL workbench建表时，字段中有PK,NN,UQ,BIN,UN,ZF,AI几个基本字段类型标识。
它们分别代表的意思是：
PK：primary key 主键
NN：not null 非空
UQ：unique 唯一索引
BIN：binary 二进制数据(比text更大)
UN：unsigned 无符号（非负数）
ZF：zero fill 填充0 例如字段内容是1 int(4), 则内容显示为0001
AI：auto increment 自增

其他GUI工具
1）sqlyog 需要收费，当然有破解版，功能最全，好用
2）navicat 有入门和收费两种，普通使用，入门就足够了。界面小清新。
3）mysql workbench 官方出的GUI，还在不断改进中，基本功能都比较稳定，也是唯一支持多平台的一个GUI


## Pycharm自带的数据插件

pycharm 使用教程（六）进行简单的数据库管理
发布于 2014-11-15 14:14:16 | 3499 次阅读 | 评论: 0 | 来源: 网友投递

本文为大家讲解的是python的编辑器pycharm 下如何进行数据库管理的方法，感兴趣的同学参考下。

功能简介：pycharm自带了一个简单的数据库插件，可以比较方便的进行简单的数据库操作。

例如：

1.创建，修改和删除数据表，字段，索引，主键，外键等。

2.提供table editor来进行数据操作

3.提供console来运行sql命令

4.提供数据导出功能

数据库创建方法

1）在pycharm的右上角找到‘database'选项卡

2）打开选项卡，按‘alt+insert'键，选择Data Source。

3）为数据库连接取一个名称，选择一个JDBC driver files。如果没有这个文件，pycharm可以自动下载。

4）选择一个JDBC driver class，mysql默认为：com.mysql.jdbc.Driver。oracle默认为：oracle.jdbc.OracleDriver

5）编写Database URL,示例：
      myql:jdbc:mysql://localhost:3306
      jdbc:oracle:thin:@localhost:1521:server

6）填写用户名和密码。

7）点击Test Connection测试连接。

8）根据提示信息修改错误，知道提示连接成功。

9）OK

参考
http://wiki.jikexueyuan.com/project/mysql-21-minutes/overview.html
