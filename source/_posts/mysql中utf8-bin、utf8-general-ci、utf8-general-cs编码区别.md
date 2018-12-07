---
title: Mysql中utf8_bin、utf8_general_ci、utf8_general_cs编码区别
date: 2017-01-29 17:00:54
tags: Mysql
---

Mysql中utf8_bin、utf8_general_ci、utf8_general_cs编码区别

在Mysql中存在着各种utf8编码格式，如下表：

1）utf8_bin

2）utf8_general_ci

3）utf8_general_cs

utf8_bin将字符串中的每一个字符用二进制数据存储，区分大小写。

utf8_genera_ci不区分大小写，ci为case insensitive的缩写，即大小写不敏感。

utf8_general_cs区分大小写，cs为case sensitive的缩写，即大小写敏感。

现在假设执行如下命令：

```
create table test_bin (

name varchar(32) not null primary key,

age int unsigned not null

) engine = InnoDB COLLATE=utf8_bin;

```
以上命令能够执行成功。

```
create table test_ci (

name varchar(32) not null primary key,

age int unsigned not null

) engine = InnoDB COLLATE=utf8_general_ci;
```

以上命令能够执行成功。

```
create table test_cs (

name varchar(32) not null primary key,

age int unsigned not null

) engine = InnoDB COLLATE=utf8_general_cs;

```
在5.6.10版本中，以上命令执行失败，不支持utf8_genral_cs。


```
insert into test_bin values('Alice', 18);
以上命令能够执行成功。

insert into test_bin values('alice', 18);
以上命令能够执行成功，因为utf8_bin是以十六进制方式存储数据，两条记录的主键不重复。

insert into test_ci values('Alice', 18);
以上命令能够执行成功。

insert into test_ci values('alily', 20);
以上命令执行失败，因为utf8_general_ci不区分大小写，两条记录的主键重复。
```
