---
title: MYSQL
date: 2016-08-15 00:06:15
tags: Database

---


## 检索

SELECT * FROM 表名

SELECT 列名,列名 FROM 表名

SELECT DISTINCT 列名 FROM 表名

SELECT -----------------LIMIT 3,4  检索第三行后的4行,就是4,5,6,7行,(注意3表示标号3的行,但第一行标号为0,实际第4行)

## 排序

SELCET prod_name FROM products ORDER BY pro_name

SELCET prod_id,prod_price,prod_name FROM products ORDER BY prod_price,prod_name  (先按价格排序,价格一样,再看名字排序)
等效于
SELCET prod_id,prod_price,prod_name FROM products ORDER BY 2,3

SELCET prod_id,prod_price,rod_name FROM products ORDER BY prod_price DESC (降序)
SELCET prod_id,prod_price,prod_name FROM products ORDER BY prod_price DESC ,prod_name

## 过滤

SELECT prod_name,prod_price FROM products WHERE 条件

## 常用条件:

> >= <  <= != AND OR NOT IN BETWEEN ,IS NULL,通配符: LIKE % _ []

注意: 既要过滤又要排序,要先过滤再排序,先WHERE,再ORDER BY

## 组合列

### 拼接

SELECT CONCAT('工号为:',FNumber,'的员工的幸福指数:',FSalary/(FAge-21))　AS employee_happiness　FROM T_Employee

### 计算

Select prod_num\*prod_price，prod_name FROM products

## 使用函数


### 数学函数
ABS(x)   返回x的绝对值
BIN(x)   返回x的二进制（OCT返回八进制，HEX返回十六进制）
CEILING(x)   返回大于x的最小整数值
EXP(x)   返回值e（自然对数的底）的x次方
FLOOR(x)   返回小于x的最大整数值
GREATEST(x1,x2,...,xn)返回集合中最大的值
LEAST(x1,x2,...,xn)      返回集合中最小的值
LN(x)                    返回x的自然对数
LOG(x,y)返回x的以y为底的对数
MOD(x,y)                 返回x/y的模（余数）
PI()返回pi的值（圆周率）
RAND()返回０到１内的随机值,可以通过提供一个参数(种子)使RAND()随机数生成器生成一个指定的值。
ROUND(x,y)返回参数x的四舍五入的有y位小数的值
SIGN(x) 返回代表数字x的符号的值
SQRT(x) 返回一个数的平方根
TRUNCATE(x,y)            返回数字x截短为y位小数的结果

### 聚合函数(常用于GROUP BY从句的SELECT查询中)
AVG(col)返回指定列的平均值
COUNT(col)返回指定列中非NULL值的个数
MIN(col)返回指定列的最小值
MAX(col)返回指定列的最大值
SUM(col)返回指定列的所有值之和
GROUP_CONCAT(col) 返回由属于一组的列值连接组合而成的结果

### 字符串函数
ASCII(char)返回字符的ASCII码值
BIT_LENGTH(str)返回字符串的比特长度
CONCAT(s1,s2...,sn)将s1,s2...,sn连接成字符串
CONCAT_WS(sep,s1,s2...,sn)将s1,s2...,sn连接成字符串，并用sep字符间隔
INSERT(str,x,y,instr) 将字符串str从第x位置开始，y个字符长的子串替换为字符串instr，返回结果
FIND_IN_SET(str,list)分析逗号分隔的list列表，如果发现str，返回str在list中的位置
LCASE(str)或LOWER(str) 返回将字符串str中所有字符改变为小写后的结果
LEFT(str,x)返回字符串str中最左边的x个字符
LENGTH(s)返回字符串str中的字符数
LTRIM(str) 从字符串str中切掉开头的空格
POSITION(substr,str) 返回子串substr在字符串str中第一次出现的位置
QUOTE(str) 用反斜杠转义str中的单引号
REPEAT(str,srchstr,rplcstr)返回字符串str重复x次的结果
REVERSE(str) 返回颠倒字符串str的结果
RIGHT(str,x) 返回字符串str中最右边的x个字符
RTRIM(str) 返回字符串str尾部的空格
STRCMP(s1,s2)比较字符串s1和s2
TRIM(str)去除字符串首部和尾部的所有空格
UCASE(str)或UPPER(str) 返回将字符串str中所有字符转变为大写后的结果

### 日期和时间函数
CURDATE()或CURRENT_DATE() 返回当前的日期
CURTIME()或CURRENT_TIME() 返回当前的时间
DATE_ADD(date,INTERVAL int keyword)返回日期date加上间隔时间int的结果(int必须按照关键字进行格式化),如：SELECTDATE_ADD(CURRENT_DATE,INTERVAL 6 MONTH);
DATE_FORMAT(date,fmt)  依照指定的fmt格式格式化日期date值
DATE_SUB(date,INTERVAL int keyword)返回日期date加上间隔时间int的结果(int必须按照关键字进行格式化),如：SELECTDATE_SUB(CURRENT_DATE,INTERVAL 6 MONTH);
DAYOFWEEK(date)   返回date所代表的一星期中的第几天(1~7)
DAYOFMONTH(date)  返回date是一个月的第几天(1~31)
DAYOFYEAR(date)   返回date是一年的第几天(1~366)
DAYNAME(date)   返回date的星期名，如：SELECT DAYNAME(CURRENT_DATE);
FROM_UNIXTIME(ts,fmt)  根据指定的fmt格式，格式化UNIX时间戳ts
HOUR(time)   返回time的小时值(0~23)
MINUTE(time)   返回time的分钟值(0~59)
MONTH(date)   返回date的月份值(1~12)
MONTHNAME(date)   返回date的月份名，如：SELECT MONTHNAME(CURRENT_DATE);
NOW()    返回当前的日期和时间
QUARTER(date)   返回date在一年中的季度(1~4)，如SELECT QUARTER(CURRENT_DATE);
WEEK(date)   返回日期date为一年中第几周(0~53)
YEAR(date)   返回日期date的年份(1000~9999)
一些示例：
获取当前系统时间：SELECT FROM_UNIXTIME(UNIX_TIMESTAMP());
SELECT EXTRACT(YEAR_MONTH FROM CURRENT_DATE);
SELECT EXTRACT(DAY_SECOND FROM CURRENT_DATE);
SELECT EXTRACT(HOUR_MINUTE FROM CURRENT_DATE);
返回两个日期值之间的差值(月数)：SELECT PERIOD_DIFF(200302,199802);
在Mysql中计算年龄：
SELECT DATE_FORMAT(FROM_DAYS(TO_DAYS(NOW())-TO_DAYS(birthday)),'%Y')+0 AS age FROM employee;
这样，如果Brithday是未来的年月日的话，计算结果为0。

### 加密函数
AES_ENCRYPT(str,key)  返回用密钥key对字符串str利用高级加密标准算法加密后的结果，调用AES_ENCRYPT的结果是一个二进制字符串，以BLOB类型存储
AES_DECRYPT(str,key)  返回用密钥key对字符串str利用高级加密标准算法解密后的结果
DECODE(str,key)   使用key作为密钥解密加密字符串str
ENCRYPT(str,salt)   使用UNIXcrypt()函数，用关键词salt(一个可以惟一确定口令的字符串，就像钥匙一样)加密字符串str
ENCODE(str,key)   使用key作为密钥加密字符串str，调用ENCODE()的结果是一个二进制字符串，它以BLOB类型存储
MD5()    计算字符串str的MD5校验和
PASSWORD(str)   返回字符串str的加密版本，这个加密过程是不可逆转的，和UNIX密码加密过程使用不同的算法。
SHA()    计算字符串str的安全散列算法(SHA)校验和
示例：
SELECT ENCRYPT('root','salt');
SELECT ENCODE('xufeng','key');
SELECT DECODE(ENCODE('xufeng','key'),'key');#加解密放在一起
SELECT AES_ENCRYPT('root','key');
SELECT AES_DECRYPT(AES_ENCRYPT('root','key'),'key');
SELECT MD5('123456');
SELECT SHA('123456');

### 控制流函数
MySQL有4个函数是用来进行条件操作的，这些函数可以实现SQL的条件逻辑，允许开发者将一些应用程序业务逻辑转换到数据库后台。
MySQL控制流函数：
CASE WHEN[test1] THEN [result1]...ELSE [default] END如果testN是真，则返回resultN，否则返回default
CASE [test] WHEN[val1] THEN [result]...ELSE [default]END  如果test和valN相等，则返回resultN，否则返回default
IF(test,t,f)   如果test是真，返回t；否则返回f
IFNULL(arg1,arg2) 如果arg1不是空，返回arg1，否则返回arg2
NULLIF(arg1,arg2) 如果arg1=arg2返回NULL；否则返回arg1
这些函数的第一个是IFNULL()，它有两个参数，并且对第一个参数进行判断。如果第一个参数不是NULL，函数就会向调用者返回第一个参数；如果是NULL,将返回第二个参数。
如：SELECT IFNULL(1,2), IFNULL(NULL,10),IFNULL(4*NULL,'false');
NULLIF()函数将会检验提供的两个参数是否相等，如果相等，则返回NULL，如果不相等，就返回第一个参数。
如：SELECT NULLIF(1,1),NULLIF('A','B'),NULLIF(2+3,4+1);
和许多脚本语言提供的IF()函数一样，MySQL的IF()函数也可以建立一个简单的条件测试，这个函数有三个参数，第一个是要被判断的表达式，如果表达式为真，IF()将会返回第二个参数，如果为假，IF()将会返回第三个参数。
如：SELECTIF(1<10,2,3),IF(56>100,'true','false');
IF()函数在只有两种可能结果时才适合使用。然而，在现实世界中，我们可能发现在条件测试中会需要多个分支。在这种情况下，MySQL提供了CASE函数，它和PHP及Perl语言的switch-case条件例程一样。
CASE函数的格式有些复杂，通常如下所示：
CASE [expression to be evaluated]
WHEN [val 1] THEN [result 1]
WHEN [val 2] THEN [result 2]
WHEN [val 3] THEN [result 3]
......
WHEN [val n] THEN [result n]
ELSE [default result]
END
这里，第一个参数是要被判断的值或表达式，接下来的是一系列的WHEN-THEN块，每一块的第一个参数指定要比较的值，如果为真，就返回结果。所有的WHEN-THEN块将以ELSE块结束，当END结束了所有外部的CASE块时，如果前面的每一个块都不匹配就会返回ELSE块指定的默认结果。如果没有指定ELSE块，而且所有的WHEN-THEN比较都不是真，MySQL将会返回NULL。
CASE函数还有另外一种句法，有时使用起来非常方便，如下：
CASE
WHEN [conditional test 1] THEN [result 1]
WHEN [conditional test 2] THEN [result 2]
ELSE [default result]
END
这种条件下，返回的结果取决于相应的条件测试是否为真。
示例：
Mysql>SELECT CASE 'green'
     WHEN 'red' THEN 'stop'
     WHEN 'green' THEN 'go' END;
SELECT CASE 9 WHEN 1 THEN 'a' WHEN 2 THEN 'b' ELSE 'N/A' END;
SELECT CASE WHEN (2+2)=4 THEN 'OK' WHEN(2+2)<>4 THEN 'not OK' END ASSTATUS;
SELECT Name,IF((IsActive = 1),'已激活','未激活') AS RESULT FROMUserLoginInfo;
SELECT fname,lname,(math+sci+lit) AS total,
CASE WHEN (math+sci+lit) < 50 THEN 'D'
WHEN (math+sci+lit) BETWEEN 50 AND 150 THEN 'C'
WHEN (math+sci+lit) BETWEEN 151 AND 250 THEN 'B'
ELSE 'A' END
AS grade FROM marks;
SELECT IF(ENCRYPT('sue','ts')=upass,'allow','deny') AS LoginResultFROM users WHERE uname = 'sue';#一个登陆验证

### 格式化函数
DATE_FORMAT(date,fmt)  依照字符串fmt格式化日期date值
FORMAT(x,y)   把x格式化为以逗号隔开的数字序列，y是结果的小数位数
INET_ATON(ip)   返回IP地址的数字表示
INET_NTOA(num)   返回数字所代表的IP地址
TIME_FORMAT(time,fmt)  依照字符串fmt格式化时间time值
其中最简单的是FORMAT()函数，它可以把大的数值格式化为以逗号间隔的易读的序列。
示例：
SELECT FORMAT(34234.34323432,3);
SELECT DATE_FORMAT(NOW(),'%W,%D %M %Y %r');
SELECT DATE_FORMAT(NOW(),'%Y-%m-%d');
SELECT DATE_FORMAT(19990330,'%Y-%m-%d');
SELECT DATE_FORMAT(NOW(),'%h:%i %p');
SELECT INET_ATON('10.122.89.47');
SELECT INET_NTOA(175790383);

### 类型转化函数
为了进行数据类型转化，MySQL提供了CAST()函数，它可以把一个值转化为指定的数据类型。类型有：BINARY,CHAR,DATE,TIME,DATETIME,SIGNED,UNSIGNED
示例：
SELECT CAST(NOW() AS SIGNED INTEGER),CURDATE()+0;
SELECT 'f'=BINARY 'F','f'=CAST('F' AS BINARY);

### 系统信息函数
DATABASE()   返回当前数据库名
BENCHMARK(count,expr)  将表达式expr重复运行count次
CONNECTION_ID()   返回当前客户的连接ID
FOUND_ROWS()   返回最后一个SELECT查询进行检索的总行数
USER()或SYSTEM_USER()  返回当前登陆用户名
VERSION()   返回MySQL服务器的版本
示例：
SELECT DATABASE(),VERSION(),USER();
SELECTBENCHMARK(9999999,LOG(RAND()*PI()));#该例中,MySQL计算LOG(RAND()*PI())表达式9999999次。



## 表处理


###　简单的方式

CREATE TABLE person (
number INT(11),
name VARCHAR(255),
birthday DATE
);

或者是

CREATE TABLE IF NOT EXISTS person (
number INT(11),
name VARCHAR(255),
birthday DATE
);

###　查看Mysql创建表:

SHOW CREATE table person;

CREATE TABLE `person` (
  `number` int(11) DEFAULT NULL,
  `name` varchar(255) DEFAULT NULL,
  `birthday` date DEFAULT NULL


###  查看表所有的列：

SHOW FULL COLUMNS from person;
+----------+--------------+-----------------+------+-----+---------+-------+---------------------------------+---------+
| Field    | Type         | Collation       | Null | Key | Default | Extra | Privileges                      | Comment |
+----------+--------------+-----------------+------+-----+---------+-------+---------------------------------+---------+
| number   | int(11)      | NULL            | YES  |     | NULL    |       | select,insert,update,references |         |
| name     | varchar(255) | utf8_general_ci | YES  |     | NULL    |       | select,insert,update,references |         |
| birthday | date         | NULL            | YES  |     | NULL    |       | select,insert,update,references |         |
+----------+--------------+-----------------+------+-----+---------+-------+---------------------------------+---------+

### 创建临时表

CREATE TEMPORARY TABLE temp_person (
number INT(11),
name VARCHAR(255),
birthday DATE
);
在创建表格时，您可以使用TEMPORARY关键词。只有在当前连接情况下，TEMPORARY表才是可见的。当连接关闭时，TEMPORARY表被自动取消。这意味着两个不同的连接可以使用相同的临时表名称，同时两个临时表不会互相冲突，也不与原有的同名的非临时表冲突。（原有的表被隐藏，直到临时表被取消时为止。）您必须拥有CREATE TEMPORARY TABLES权限，才能创建临时表。


###　如果表已存在，则使用关键词IF NOT EXISTS可以防止发生错误。


CREATE TABLE IF NOT EXISTS person2 (
number INT(11),
name VARCHAR(255),
birthday DATE
);

注意，原有表的结构与CREATE TABLE语句中表示的表的结构是否相同，这一点没有验证。注释：如果您在CREATE TABLE...SELECT语句中使用IF NOT EXISTS，则不论表是否已存在，由SELECT部分选择的记录都会被插入。

### 在一个表的基础上创建表

在CREATE TABLE语句的末尾添加一个SELECT语句，在一个表的基础上创建表
CREATE TABLE new_tbl SELECT * FROM orig_tbl;

注意，用SELECT语句创建的列附在表的右侧，而不是覆盖在表上

Mysql> SELECT * FROM foo;
+---+
| n |
+---+
| 1 |
+---+
Mysql> CREATE TABLE bar (m INT) SELECT n FROM foo;
Mysql> SELECT * FROM bar;
+------+---+
| m    | n |
+------+---+
| NULL | 1 |
+------+---+

也可以明确地为一个已生成的列指定类型
CREATE TABLE foo (a TINYINT NOT NULL) SELECT b+1 AS a FROM bar;

### 根据其它表的定义（包括在原表中定义的所有的列属性和索引），使用LIKE创建一个空表:

CREATE TABLE new_tbl LIKE orig_tbl;

### 创建一个有主键，唯一索引，普通索引的表:

CREATE TABLE `people` (
  `peopleid` smallint(6) NOT NULL AUTO_INCREMENT,
  `firstname` char(50) NOT NULL,
  `lastname` char(50) NOT NULL,
  `age` smallint(6) NOT NULL,
  `townid` smallint(6) NOT NULL,
  PRIMARY KEY (`peopleid`),
  UNIQUE KEY `unique_fname_lname`(`firstname`,`lastname`),
  KEY `fname_lname_age` (`firstname`,`lastname`,`age`)
) ;


其中peopleid是主键,以firstname和lastname两列建立了一个唯一索引,以firstname,lastname,age三列建立了一个普通索引

### 删除表

DROP TABLE  tbl_name;
或者是
DROP TABLE IF EXISTS tbl_name;

## 视图

http://www.cnblogs.com/chenpi/p/5133648.html

SQL 测验
结果：17/20
您的回答：
1.SQL 指的是？
您的回答：Structured Query Language
2.哪个 SQL 语句用于从数据库中提取数据？
您的回答：SELECT
3.哪条 SQL 语句用于更新数据库中的数据？
您的回答：UPDATE
4.哪条 SQL 语句用于删除数据库中的数据？
您的回答：DELETE
5.哪条 SQL 语句用于在数据库中插入新的数据？
您的回答：INSERT INTO
6.通过 SQL，您如何从 "Persons" 表中选取 "FirstName" 列？
您的回答：SELECT FirstName FROM Persons
7.通过 SQL，您如何从 "Persons" 表中选取所有的列？
您的回答：SELECT * FROM Persons
8.通过 SQL，您如何从 "Persons" 表中选取 "FirstName" 列的值等于"Peter" 的所有记录？
您的回答：SELECT * FROM Persons WHERE FirstName='Peter'
9.通过 SQL，您如何从 "Persons" 表中选取 "FirstName" 列的值以 "a" 开头的所有记录？
您的回答：SELECT * FROM Persons WHERE FirstName LIKE '%a'
正确答案：SELECT * FROM Persons WHERE FirstName LIKE 'a%'
10.请判断下列说法是否正确：当所列出的某个条件为 true 时，OR 运算符会显示记录。当列出的所有条件为 true 时，AND 运算符会显示记录。
您的回答：正确
11.通过 SQL，您如何在表 Persons 中选择 FirstName 等于 Thomas 而 LastName 等于 Carter 的所有记录？
您的回答：SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'
12.通过 SQL，您如何按字母顺序选取 Persons 表中 LastName 介于 Adams 和 Carter 的所有记录？
您的回答：SELECT * FROM Persons WHERE LastName BETWEEN 'Adams' AND 'Carter'
13.哪条 SQL 语句可返回唯一不同的值？
您的回答：SELECT UNIQUE
正确答案：SELECT DISTINCT
14.哪个 SQL 关键词用于对结果集进行排序？
您的回答：ORDER BY
15.通过 SQL，您如何根据 "FirstName" 列降序地从 "Persons" 表返回所有记录？
您的回答：SELECT * FROM Persons ORDER BY FirstName DESC
16.通过 SQL，您如何向 "Persons" 表插入新的记录？
您的回答：INSERT VALUES ('Jimmy', 'Jackson') INTO Persons
正确答案：INSERT INTO Persons VALUES ('Jimmy', 'Jackson')
17.通过 SQL，您如何向 "Persons" 表中的 "LastName" 列插入 "Wilson" ？
您的回答：INSERT INTO Persons (LastName) VALUES ('Wilson')
18.您如何把 "Persons" 表中 "LastName" 列的 "Gates" 改为 "Wilson" ？
您的回答：UPDATE Persons SET LastName='Wilson' WHERE LastName='Gates'
19.通过 SQL，您如何在 "Persons" 表中删除 "FirstName" 等于 "Fred" 的纪录？
您的回答：DELETE FROM Persons WHERE FirstName = 'Fred'
20.通过 SQL，您如何返回 "Persons" 表中记录的数目？
您的回答：SELECT COUNT(*) FROM Persons


http://www.cnblogs.com/mr-wid/archive/2013/05/09/3068229.html
