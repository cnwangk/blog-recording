---
title: SQL基础知识扫盲
date: 2023-03-16 18:49:22
tags: SQL
categories: 
- [数据库]       
---

此篇总结是对之前发出的 SQL是什么 进行补充。

进入正题之前，我想聊聊其它的知识点，一点点思考。

学习某个技能点或者是新知识点时，可以尝试建立一项知识梳理体系，如下：

1. **输入**：可以照葫芦画瓢，亲自动手实践。
2. **分析**：有自己独立的分析和思考。
3. **输出**：产出的内容与预期进行对比。
4. **札记**：记录收获过程（手写或者以电子文档形式记录）。

这张流程图制作比较粗糙，权当梳理基本知识参考。

上面也谈到了，学习新知识点。善于总结，可以使用流程图或者思维导图构建知识体系。

[![pp8KvDg.png](https://s1.ax1x.com/2023/03/16/pp8KvDg.png)](https://imgse.com/i/pp8KvDg)



# SQL & 数据库基础知识扫盲



一般而言，在日常工作交流中，大家所描述的SQL是标准SQL（Standardized SQL），非特指某一数据库厂商（DBMS）专有语言。



### SQL是什么？

SQL必知必会这样描述到：

**SQL**（发音为字母S-Q-L或sequel）是Structure Query Language（**结构化查询语言**）的缩写。SQL是一种专业用于与数据库沟通交互的语言。

与其他语言（比如英语或者Java、C、PHP这类编程语言）不一样，SQL中只有很少的词，这是有意而为。设计SQL的目的是便于完成一项任务，提供一种**从数据库中读写数据的简单有效方法**。

用一句话总结：SQL是Structure Query Language（**结构化查询语言**）。



维基百科这样描述到：

1. 全称是Structure Query Language（**结构化查询语言**）是一种**特定目的编程语言**，一般简称为**SQL**。

2. **用于管理关系数据库管理系统**（RDBMS）。它是使用**关系模型的数据库应用语言**，由IBM在20世纪70年代开发出来，作为IBM数据库System R的原型关系语言，**实现数据库中信息检索**。

3. 20世纪80年代初，美国国家标准学会（ANSI）开始着手定制SQL标准。最早的ANSI始于1986年，被称为SQL-86，在1987年成为国际标准化组织（ISO）标准。尽管SQL并非完全按照科德的关系模型设计，但其依然成为最为广泛运用的数据库语言。此后，这一标准经过了一系列的增订，加入了大量新特性。虽然有这一标准的存在，但大部分的SQL代码在不同的数据库系统中并不具有完全的跨平台性。

   

用我自己的经验总结概括：其实是将数据有规律地存放在特定容器中的一种结构化查询语言。



**SQL有哪些优点呢**？

1. SQL不是某一特定数据库厂商专有语言。绝大多数流行的DBMS支持SQL，所以学习标准SQL可以让你和大多数数据库打交道。
2. SQL简单易学。它的语句是有很强描述性的英语单词组成，而这些单词数目不多。
3. SQL看上去（入门）很简单，实际上是一种强有力的语言，灵活使用其语言元素，可以进行非常复杂和高级的数据库操作。



**SQL扩展说明**：许多DBMS厂商通过增加语句或指令，对SQL进行扩展，目的是提供执行特定操作的额外功能或简化方法。虽然这种扩展使用很便捷，但一般情况是针对个别DBMS，很少有两个厂商同时支持这种扩展。列举两个例子，比如Oracle分页可以使用rownum实现，而MySQL分页使用limit关键字。



### 数据库是什么？

**数据库**

数据库（database）：保存有组织数据的容器，通常是一个文件或一组文件。

**tips**：通常说数据库指关系型数据库（RDBMS）。

**注意混淆**平时工作交流，大家通常用数据库这个术语来代表使用的数据软件，这种表述不完全正确，因此产生了许多混淆。确切地说，数据库软件指**数据库管理系统（DBMS）** 。数据库是通过DBMS创建和操作的容器，它具体是什么，形式如何，各种数据库有所差异。这种差异表现在：各大数据库厂商基于标准SQL进行各自的扩展。

**简易说明**
在MySQL中创建数据库语法：`create database db_name`。而在Oracle数据库中创建数据库语法`create user db_name`，你没看错，Oracle中基于用户进行描述与管理。如果你在Oracle中使用`create database db_name`，会提示数据库已装载。



**表**

表（table）：某种特定类型数据库结构化清单。



**表名**

表名（table name）：**表名是唯一的**（不可重复），实际上是数据库名和表名等的组合，数据库名理解为用户会容易接受一点。有的数据库使用数据库拥有者的名字作为唯一名的一部分，例如Oracle、达梦数据库。在同一个数据中不能使用相同的表名，但在不同的数据库中可以使用相同的表名。



**模式**

模式：关于数据库和**表的布局及特性**的信息。



**列**

列（column）：**表中的一个字段**。所有表由一个列或多列组成。

数据分解：合理将数据分解为多个列尤为重要。例如：城市、州、邮政编码总是彼此独立的列。通过分解这些数据，才有可能利用特定的列对数据进行分类和过滤（比如找出特定州或城市的所有顾客）。如果城市和州组合到一个列中，则按州分类或过滤会很困难。

当然，你可以根据自己的需求将数据分解到何种程度。例如，一般可以将街道名和门牌号一起存储到地址里，没有特殊需求是可以这样处理。如果那一天，需求发生变化，根据门牌号进行排序或过滤，最好将门牌号和街道名分开。



**数据类型**

数据类型：允许哪一种数据类型。每一张表中列具有相应数据类型，限制（或允许）该列中存储哪一种类型的数据。



**行**

行（row）：表中列一条或多条记录。



**主键**

主键（primary key）：一列（或几列），其值可以唯一标识表中每一行。

定义主键：或许并不总是需要主键，达到便于管理目的，大多数数据设计者会保证他们创建的每张表具有一个主键。



**外键**

外键（foreign key）：用来保证参照完整性，通常在两张或多张表中存在。如果有两张表：主表（parent table）和子表（child table），在子表中拥有主表外键约束；你想同时删除两张表；MySQL提示需要先删除约束，才能彻底删除。也有例外，比如设置了级联（cascade）。



**理论知识看得再多，不如亲自实践一遍，效果来得更快**。



### 挺身入局，实践出真知

**选择**

1. 选择：选择一种**流行**且**社区活跃**DBMS厂商发行版数据库软件进行入门。
2. 安装：云服务器或者本机亦或是**虚拟机模拟环境**。
3. 初学：建议使用各大厂商自带GUI**字符命令界面**进行交互。

**推荐**

个人推荐学习MySQL（MariaDB），逐步学习，深入浅出。为什么推荐入门首选学习MySQL，上面提到了**流行**、**社区活跃**，换句话说，MySQL资源丰富，官方文档全面，更新频繁。



**关于CRUD：增删查改**

一般而言，CRUD是指对数据库表行记录进行新增（insert）、删除（delete）、查询（select）以及修改（update）操作。



**各大DBMS厂商数据库官方文档地址整合**：

[https://blog.cnwangk.top/2022/03/17/MySQL等主流数据库厂商（DBMS）-官方文档地址](https://blog.cnwangk.top/2022/03/17/MySQL等主流数据库厂商（DBMS）-官方文档地址)





# DBMS初体验

1. MySQL（MariaDB）
2. Oracle
3. postgreSQL

### MySQL：初体验

1. 部署MySQL；
2. 检验（启动与关闭服务）；
3. 修改密码与权限（为第5步做准备）；
4. 字符命令界面进行交互；
5. 工具：MySQL workbench、DBeaver（通用数据库管理器）或者SQLyog；
6. 基本操作（CRUD：insert、delete、update、select）；
7. 参考官方文档 & 官方完整Demo示例。



**部署MySQL8.0.x**

**Windows install MySQL8.0.x (Archive zip) 简易安装教程**

1. 解压免安装版MySQL：unzip mysql-8.0.x-winx64.zip
2. 切换到MySQL解压目录：cd mysql-8.0.x-winx64
2. 新增MySQL配置文件： my.ini
3. 初始化MySQL：bin\mysqld --initialize-insecure 或者 bin\mysqld --initialize-insecure --console 
4. 注册MySQL服务：bin\mysqld --install MySQL80（将MySQL服务注册到service，可以使用net命令进行管理）
5. 启动MySQL服务：net start MySQL80 或者 sc start MySQL80
6. 登录MySQL字符管理界面：mysql -uroot -p



**注意**：版本选择：带有GA（General Availability）标识为稳定版，目前最新稳定是MySQL 8.0.32 发布于2023-01-17。x代表使用MySQL8.0具体版本。打开CMD或者Powershell时以管理员身份运行，如果没有，安装服务时则会提示权限拒绝，如下所示。

D:\mysql-8.0.32-winx64\bin>mysqld --install MySQL80
Install/Remove of the Service Denied!



Windows环境新建my.ini做如下设置，指定基本安装目录与数据存放目录：

```bash
[mysqld]
basedir=D:\\mysql-8.0.32-winx64
datadir=D:\\mysql-8.0.32-winx64\\data
```



**登录到命令行字符界面**

Windows 平台打开CMD、Powershell或者Windows terminal（win + x 打开Windows终端（管理员））

**参数作用**：

- -u：指定用户为root。
- -p ：回车后输入密码，如果直接输入密码回车即可登录。
- -P ：指定端口号（port），默认为3306。

Windows平台修改my.ini指定MySQL server端口，Linux平台修改my.cnf指定端口。

```bash
mysql -uroot -p -P 3306
```

Linux发行版打开终端（terminal）

```bash
mysql -uroot -p -P 3306
```

**输入**：

```sql
mysql> select 1\G
```

**分析**：

登录到MySQL字符操作界面，输入select 1\G、select 1；或者select 1\g，会得到输出内容：1。这种情况MySQL不用访问表或索引，直接得到结果，通过explain使用执行计划（后续可以了解）可以看出type=NULL，此时效率最高。

**输出**：

```sql
*************************** 1. row ***************************
1: 1
1 row in set (0.00 sec)
```

提示：同样在postgreSQL中也是支持select 1；或者select 1\g，输出结果：1。



**做笔记：SQL CRUD**

在创建数据库（用户)、表，最好统一大小写、驼峰命名、下划线，不要混搭使用。个人给出的建议是：要么纯大写，要么纯小写，要么使用下划线进行分割。**使用拼音命名库名、表名、字段名的时候（最好不要简写），如果简写，也请写好注释**。比如地标性的命名北京（beijing）、上海（shanghai）、广州（guangzhou）、深圳（shenzhen），使用全拼音这是可以的，即便查询字典大概也是这样命名的，最好与你的合作团队达成统一意见。

当然，你看到我所演示SQL语句，关键字部分统一使用大写，库名、表名、字段名使用小写。

**注释使用**

```sql
/** MySQL基础知识扫盲 **/
-- MySQL基础知识扫盲
```



**创建数据库**

创建管理用户study（习惯叫数据库），注意: 执行更新操作时，时刻牢记数据无价，指定条件。最大程度避免给自己带来不必要的工作麻烦。

```sql
CREATE DATABASE study;
```

**切换用户**

```sql
USE study;
```

**建表语句**

创建表，在study用户下分别创建表：girl、books。

```sql
CREATE TABLE study.girl(
    id INT  PRIMARY KEY,
    girl_name VARCHAR(64),
    girl_age VARCHAR(64),
    cup_size VARCHAR(64),
    stu_num VARCHAR(64) 
)

CREATE TABLE study.books(
    id VARCHAR(32) NOT NULL PRIMARY KEY,
    book_names VARCHAR(64) NOT NULL,
    isbn VARCHAR(64) NOT NULL,
    author VARCHAR(16) NOT NULL
);
```



**第一张表girl**：使用CRUD语句 & 开启显式开启事务（MySQL & MariaDB默认开启自动autocommit提交）。

**显式开启事务**

```sql
BEGIN;
-- start transaction;
```

**查询**：标准写法，**指定字段名**

```sql
SELECT sg.id,sg.girl_name,sg.girl_age,sg.cup_size,sg.stu_num FROM study.girl sg;
```

查询：偷懒写法

```sql
SELECT * FROM study.girl sg;
```

**插入**一条数据：标准写法，**指定字段名**

```sql
INSERT INTO study.girl(id,girl_name,girl_age,cup_size,stu_num) VALUES(1001,'梦梦','16','B','tolovemm16');
```

插入一条数据：偷懒写法

```sql
INSERT INTO study.girl VALUES(1001,'梦梦','16','B','tolovemm16');
```

**删除**数据：指定条件

```sql
DELETE FROM study.girl sg WHERE sg.id=1001;
```

**修改**数据：指定条件

```sql
UPDATE study.girl(id,girl_name,girl_age,cup_size,stu_num) sg SET sg.stu_num='toloveC16'  WHERE sg.id=1001;
UPDATE study.girl sg SET sg.cup_size='C'  WHERE sg.id=1001;
```

**回滚**操作

```sql
ROLLBACK;
```

**提交**事务

```sql
COMMIT;
```



**第二张表books**：

```sql
-- 插入
INSERT INTO study.books VALUES('1001','books','2023-3-15-miji','张三');

-- 修改
UPDATE study.books b  SET b.book_names='绝世武功秘籍' WHERE b.id='1001'; 

-- 查询
SELECT * FROM study.books;
-- 不用带上用户名也能查询，切换用户操作：use study
SELECT * FROM books;

-- 删除全表数据内容
DELETE FROM study.books;

-- 删除全表数据内容：TRUNCATE [TABLE] tbl_name
TRUNCATE TABLE study.books;

-- 删除表结构与内容,注意：无法回滚
DROP TABLE study.books; 
```








**MySQL官方完整Demo示例**

最后附上官方示例数据库，**sakila-db数据库**一个非常完整的示例。包含：视图、函数、触发器以及存储过程，当然也存在使用外键。

**sakila-db数据库**包含三个文件，便于大家获取与使用：

1. sakila-schema.sql：数据库表结构；
2. sakila-data.sql：数据库示例模拟数据；
3. sakila.mwb：数据库物理模型，在MySQL workbench中可以打开查看。

> [https://downloads.mysql.com/docs/sakila-db.zip](https://downloads.mysql.com/docs/sakila-db.zip)



**用于用于简单测试学习，可以使用world-db**：

**world-db数据库**，包含三张表：city、country、countrylanguage。

> [https://downloads.mysql.com/docs/world-db.zip](https://downloads.mysql.com/docs/world-db.zip)



MySQL官方文档（5.6、5.7、8.0）整合：

链接: https://pan.baidu.com/s/18TPW7Lan2WoJhHxWJUM3cw?pwd=bx44 

提取码: bx44 





### Oracle：初体验

初步使用，建议掌握Oracle自带的字符命令操作工具 SQL plus。

其次掌握第三方管理工具 PLSQL developer，管理Oracle很好用，免费30天试用，付费软件。

个人认为，有必要了解Oracle自带SQL客户端管理工具SQL developer，免费使用。

1. SQL plus
2. PLSQL developer
3. SQL developer



以下将演示在Oracle数据库中如何构建用户、表、对数据查询、新增、修改、删除操作。

**1、创建用户**

创建数据库test，在Oracle中指创建用户用于管理

常规（Oracle12c是一个拐点，有CDB和PDB之分）建表用法：

```sql
create user test identified by 123456;
```

新版Oracle19c（带c，默认为CDB模式），新建用户

```sql
create user c##test identified by 123456;
```



**2、授权**

授予用户test权限resource，connect

```sql
grant resource,connect to test;
```

**3、建表**

创建表girl，指定了用户为test

```sql
 create table test.girl(
     ID VARCHAR2(32) not null,
     GIRL_NAME VARCHAR2(64),
     GIRL_SEX VARCHAR2(2)
 )
```

**4、索引**

添加主键索引

```sql
 alter table test.girl add primary key(ID);
```

**5、查询、新增、修改、删除**

查询表girl

```sql
 select * from test.girl;
```

新增数据

```sql
 insert into test.girl values('1001','梦梦','女');
```

修改数据

```sql
 update test.girl t set t.ID='1002';
```

删除数据

删除表中全部数据，但不删除表结构。使用drop则删除表结构以及数据。
```sql
 delete from test.girl;
```





### PostgreSQL：初体验

主要熟悉PostgreSQL自带的SQL shell字符命令工具和pgAdmin客户端管理工具的使用。

1. SQL shell
2. pgAdmin

可以在我个人公众号历史文章中找到关于PostgreSQL入门教程。



### Demo示例

**SQL必知必会demo示例**

官网地址：https://forta.com/books/0135182794/

涵盖DBMS示例：DB2、SQLserver、MySQL、Oracle、PostgreSQL、SQLite

**SQL表结构示例下载**

个人整理一些资料进行整合打包。

链接: https://pan.baidu.com/s/1MHVa-oo22XKJoLmf7NrU4A	

提取码: cx3p 





**参考资料**：

1. SQL必知必会第5版。



最后，以上总结仅供参考哟！

**——END——**
