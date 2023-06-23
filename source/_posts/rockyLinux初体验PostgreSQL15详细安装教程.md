---
title: rockyLinux初体验PostgreSQL15详细安装教程
date: 2023-04-26 22:07:49
tags: PostgreSQL
categories:
- [数据库]
---

![](https://s1.ax1x.com/2023/04/25/p9KFODs.png)

**原创计划  | 总第 11 期（2023 第 09 期）知识分享**

 **rockyLinux 安装 PostgreSQL 15.2**

**作者 | 文正耕耘（ID：dywangk）**



彼时，PostgreSQL 已经更新到了15.2。在rockyLinux上初体验PostgreSQL15，从部署到测试psql工具，体验基本用法，运用通用数据库管理工具。

<!-- more -->

距离我上一次写 PostgreSQL 教程 2022-03-20，已经过去一年多了。Linux篇 PostgreSQL 教程很久之前就想写了，一直停留在想法上面，没有付诸实际行动。那会我的主要环境还在centos-7上，因为 centos-7快要停止维护了，目前已经转移到 rockyLinux-9平台。

当时只是简单的在 Windows 平台介绍如何安装和简单使用，甚至没有过多参考官方文档。

也是对前段时间总结的 《SQL 基础知识扫盲》 的补充。

如今，我为什么又写起了 postgreSQL 相关文档呢？
答：目前市面postgreSQL文档相对较少，官方文档纯英文，上手有一定的难度。像MySQL（MariaDB）、Oracle之类的文档已经烂大街了，无非是新版本发布，闲暇时间部署尝尝鲜。



初体验，第一次嘛，姿势、动作难度不能太高，容易劝退，所以比较简单。



### 数据库软件 PostgreSQL 安装

如果获取软件比较缓慢，可以在公众号回复blog，进入站点搜索：rockyLinux镜像源下载地址。如下所示，列出部分 postgresql 国内镜像源地址：

1. 浙江大学开源软件镜像站：[https://mirrors.zju.edu.cn/postgresql/](https://mirrors.zju.edu.cn/postgresql/)
2. 中国科学技术大学镜像站：[https://mirrors.ustc.edu.cn/postgresql/](https://mirrors.ustc.edu.cn/postgresql/)
3. 清华大学开源软件镜像站：[https://mirrors.tuna.tsinghua.edu.cn/postgresql/](https://mirrors.tuna.tsinghua.edu.cn/postgresql/)

最新版本（PDF）文档地址：[https://www.postgresql.org/files/documentation/pdf/15/postgresql-15-A4.pdf](https://www.postgresql.org/files/documentation/pdf/15/postgresql-15-A4.pdf)

如果还是下载缓慢，这是正常现象，建议使用迅雷（打钱）等BT工具下载，或者在Linux平台使用 wget 获取，然后使用 scp 命令传到Windows平台浏览。


目前所有版本，最新版本为15.2，9th February 2023: PostgreSQL 15.2, 14.7, 13.10, 12.14, and 11.19 Released!



**安装方式：Packages and Installers**

使用 Installers 安装包形式进行安装，RHEL系列使用rpm包居多。

选择适合你的操作系统，支持的操作系统比较丰富：

1. Linux
2. macOS
3. Windows
4. BSD
5. Solaris



postgreSQL 下载目前支持两种方式：

1. Packages：发行安装包形式，难易度较低，不灵活。
2. Source：源码包形式，难易度相对较高，比较灵活。


如下，将演示Linux发行版Rocky-9平台PostgreSQL的部署。


切换到普通用进行安装：
```bash
su wzgy
```

如果安装rockyLinux-9之后，默认提示安装的版本是 postgresql-13.10，使用TAB键进行补全会提示。
```bash
[wzgy@localhost ~]$ dnf -y install postgresql-server-13.10-1.el9_1.x86_64
postgresql-contrib-13.10-1.el9_1.x86_64   
...
postgresql-server-13.10-1.el9_1.x86_64	postgresql-upgrade-13.10-1.el9_1.x86_64
```


如果想安装比较新的版本，可以前往postgresql官网找到对应的Linux发行版选择对应版本进行安装。

postgreSQL 下载地址： [https://www.postgresql.org/download/](https://www.postgresql.org/download/)

示例选择 Linux 发行版**Red Hat/Rocky/CentOS version 9**（版本），**PostgreSQL Yum**源仓库：
[https://www.postgresql.org/download/linux/redhat/](https://www.postgresql.org/download/linux/redhat/)

**PostgreSQL 快速安装**

```bash
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
sudo dnf -qy module disable postgresql
sudo dnf install -y postgresql15-server
sudo /usr/pgsql-15/bin/postgresql-15-setup initdb
sudo systemctl enable postgresql-15
sudo systemctl start postgresql-15
```



**PostgreSQL 详细安装步骤**

**PostgreSQL 下载所需要 rpm 依赖包，用于更新（版本库）到最新版本**：

```bash
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```

**PostgreSQL 导入公钥，验证过程，由于网络等原因可能会失败**：

```bash
sudo dnf -qy module disable postgresql
导入 GPG 公钥 0x442DF0F8:
 Userid: "PostgreSQL RPM Building Project <pgsql-pkg-yum@postgresql.org>"
 指纹: 68C9 E2B9 1A37 D136 FE74 D176 1F16 D2E1 442D F0F8
 来自: /etc/pki/rpm-gpg/RPM-GPG-KEY-PGDG
```

**PostgreSQL 安装 postgresql-15 服务**

```bash
sudo dnf install -y postgresql15-server
```
由于网络等原因，**可能安装会比较缓慢**，这里建议更换为国内yum & dnf 源，比如阿里、网易等等都可以。

**比如更换阿里源**：

```bash
sed -e 's|^mirrorlist=|#mirrorlist=|g' \
    -e 's|^#baseurl=http://dl.rockylinux.org/$contentdir|baseurl=https://mirrors.aliyun.com/rockylinux|g' \
    -i.bak \
    /etc/yum.repos.d/rocky-*.repo
dnf makecache
```

**注意**：替换镜像源，建议先备份，然后验证路径是否正确。

示例，注意大小写，可能存在无法读取正确路径，**Linux下对大小写敏感**：
```bash
ls /etc/yum.repos.d/rocky-*.repo
```
输出信息：/etc/yum.repos.d/rocky-addons.repo   /etc/yum.repos.d/rocky-devel.repo   /etc/yum.repos.d/rocky-extras.repo，证明路径真实存在。

备份，sed命令接 -i 属性已经加入备份到当前目录：
```bash
sed -i .bak \
/etc/yum.repos.d/rocky-*.repo
```
最后使用 dnf makecache 更新缓存：
```bash
dnf makecache
```
如果使用 RHEL8 之前，请使用 yum makecache 更新。



**PostgreSQL 初始化**：

```bash
/usr/pgsql-15/bin/postgresql-15-setup initdb
```
看到：Initializing database ... OK，证明初始化完成。

为什么这样执行？
答：postgresql-15-setup 脚本所在绝对路径位置 /usr/pgsql-15/bin/，通过 initdb 参数进行初始化。

如果你有过使用MySQL（MariaDB）或者Oracle以及其它关系型数据库经验，也存在初始化的过程，执行命令略有不同。在MySQL（MariaDB）中，可以使用如下命令初始化：bin\mysqld –initialize-insecure 或者 bin\mysqld –initialize-insecure –console。



**PostgreSQL 设置开机自启**

```bash
systemctl enable postgresql-15
```
看到输出信息：Created symlink /etc/systemd/system/multi-user.target.wants/postgresql-15.service → /usr/lib/systemd/system/postgresql-15.service. 代表设置开机自启完成。

**PostgreSQL 服务启动**

```bash
systemctl start postgresql-15
```



查询当前用户身份：

```bash
bash-5.1$ whoami
postgres
```

可以看到当前用户已经切换到了 postgres。



**管理 PostgreSQL 服务另一种方式，使用 pg_ctl 脚本**

pg_ctl  命令启动服务：

```bash
bash-5.1$ /usr/pgsql-15/bin/pg_ctl -D /var/lib/pgsql/15/data/ start
```

![](https://s1.ax1x.com/2023/04/25/p9KFxU0.png)

输出信息：

> 等待服务器进程启动 ....2023-04-25 18:47:50.476 CST [3505] 日志:  日志输出重定向到日志收集进程
> 2023-04-25 18:47:50.476 CST [3505] 提示:  后续的日志输出将出现在目录 "log"中.
>  完成
> 服务器进程已经启动



pg_ctl  命令重启服务：

```bash
bash-5.1$ /usr/pgsql-15/bin/pg_ctl -D /var/lib/pgsql/15/data/ restart
```

输出信息：

> 等待服务器进程关闭 .... 完成
> 服务器进程已经关闭
> 等待服务器进程启动 ....2023-04-25 18:48:34.629 CST [3521] 日志:  日志输出重定向到日志收集进程
> 2023-04-25 18:48:34.629 CST [3521] 提示:  后续的日志输出将出现在目录 "log"中.
>  完成
> 服务器进程已经启动



pg_ctl  命令停止服务：

```bash
bash-5.1$ /usr/pgsql-15/bin/pg_ctl -D /var/lib/pgsql/15/data/ stop
```

输出信息：

> 等待服务器进程关闭 .... 完成
> 服务器进程已经关闭



**注意**：需要以非 root 用户身份执行命令。

> pg_ctl: 无法以 root 用户运行
> 请以服务器进程所属用户 (非特权用户) 登录 (或使用 "su")





### 数据库软件 PostgreSQL 配置

**postgreSQL 查看状态以及验证是否自启**
```bash
systemctl enable postgresql-15
```
当你看到 active (running)，代表服务（活跃）正常启动状态，看到 /usr/lib/systemd/system/postgresql-15.service; enabled;代表开机自启，如果想开机禁用，使用命令 systemctl disable postgresql-15 即可。

到此为止，postgresql-15 安装过程以及服务启动演示完成。



**postgresql-15 初步使用**

**rockyLinux创建普通用户**，需要root（创建用户）权限：

```bash
useradd wzgy
passwd wzgy
```
参数含义：
1. useradd wzgy：useradd 命令用于新增用户，后面接用户名。
2. passwd wzgy：passwd 命令用于修改新增用户密码。



**切换到普用户**，如果没有普通用户，可以创建一个用户用于安装管理postgresql-15：

```bash
su wzgy
sudo systemctl status postgresql-15.service
```
参数含义：
1. su wzgy：su 命令用切换用户身份。
2. sudo：用于提取权限，是一个很有意思的命令。

**netstat 监控 5432 端口**，输出信息如下：

```bash
[wzgy@localhost ~]$ sudo netstat -tlunp | grep 5432
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN      9117/postmaster
tcp6       0      0 ::1:5432                :::*                    LISTEN      9117/postmaster
```

![](https://s1.ax1x.com/2023/04/25/p9KFHgg.png)



**ps 监控服务命令监控 postmaster服务**：

```bash
ps -aux | grep postmaster
```

![](https://s1.ax1x.com/2023/04/25/p9KkpCT.png)

通过监控服务命令可以看出，初始化的data目录在：/var/lib/pgsql/15/data/。



使用 yum & dnf 命令安装，**默认配置文件所在路径**：

```bash
/var/lib/pgsql/15/data/postgresql.conf
```

**注意**：如果 data 目录不存在，大概率初始化阶段出现问题，也就是初始化失败，需要检查日志文件：/var/lib/pgsql/15/initdb.log。



服务器环境可以使用 vim 或者 nvim（需要安装 neovim ）进行编辑配置文件：postgresql.conf。

修改配置：sudo vim /var/lib/pgsql/15/data/postgresql.conf

开放配置，只演示最基础的：

1. listen_addresses = 'localhost' ：监听地址，重启数据库软件服务生效；
2. defaults to 'localhost'; use '*' for all：**默认为localhost，\*代表开放所以ip进行访问**。
3. port = 5432 ： 监听端口，重启数据库软件服务生效；
4. max_connections = 100 ：最大连接数，重启数据库软件服务生效。

```bash
# - 配置文件：连接设置 -
listen_addresses = 'localhost'          # 监听地址，重启数据库软件服务生效;
port = 5432                             # 监听端口，重启数据库软件服务生效;
max_connections = 100                   # 最大连接数，重启数据库软件服务生效;
```

![](https://s1.ax1x.com/2023/04/25/p9Kk98U.png)



**注意**：如果需要使用通用数据库管理工具远程连接，还需要做如下修改，授予相应权限，由于测试，我直接设置 all（所有ip）：

![](https://s1.ax1x.com/2023/04/25/p9KFz5V.png)

编辑pg_hba.conf配置文件，vim /var/lib/pgsql/15/data/pg_hba.conf，找到 IPv4 local connections，官方文档有详细配置说明。理论上，应该可以通过 GRANT 命令形式授权，在MySQL（MariaDB）是支持的。

```bash
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
host    all             all             all                     scram-sha-256
```

如果安装了 firewalld 防火墙管理工具，需要开放相应的端口：

```bash
firewall-cmd --zone=public --add-port=5432/tcp --permanent
firewall-cmd --reload
```

![](https://s1.ax1x.com/2023/04/25/p9KFHgg.png)



**修改配置文件后，记得重启 postgresql 服务**。



如果你使用其它普通用户创建用户、角色、登录等等操作，会出现如下错误：
createuser: 错误: 连接到套接字"/var/run/postgresql/.s.PGSQL.5432"上的服务器失败:致命错误:  角色 "root" 不存在。



如果你不确定有哪些用户，可以使用命令查看：

```bash
[root@localhost ~]# cat /etc/passwd | grep postgres
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
```
**请注意**：有时候为了方便，我直接使用root用户操作，比如我用 cat 和 grep 命令查看postgres用户。

解决方案，**切换用户为postgres：su postgres**，如果你仔细阅读了官方文档，其实会有启发的。

登录字符命令操作界面 psql：
```bash
psql
```



### 数据库软件 PostgreSQL 交互

参数 postgres=#：登录 PostgreSQL 默认用户前缀名称。

输入 select version(); 查询版本：
```bash
postgres=# select version();
```
输出信息：PostgreSQL 15.2 on x86_64-pc-linux-gnu, compiled by gcc (GCC) 11.3.1 20220421 (Red Hat 11.3.1-2), 64-bit。

参数含义：
1. PostgreSQL 15.2：数据库软件版本 15.2。
2. x86_64-pc-linux-gnu：使用Linux平台x86_64架构。
3. compiled by gcc (GCC) 11.3.1 20220421 (Red Hat 11.3.1-2)：编译gcc版本。
4. 64-bit：64位操作系统。

输入测试验证：postgres=# select 1\g
输出结果： ?column? 	1，这是正常状态。



**创建表 books**

```sql
postgres=# create table books(id varchar(64) primary key,name varchar(64));
CREATE TABLE
```



**新增操作**，插入一条数据：

```sql
postgres=# insert into books values('1001','绝世武功秘籍');
INSERT 0 1
```



**查询操作**，查询表 books ：

```sql
postgres=# select * from books\g
  id  |     name
------+--------------
 1001 | 绝世武功秘籍
(1 行记录)
```


**修改操作**，修改表  books ：

```sql
postgres-# update books set name='PostgreSQL-15.2'  where id='1001'
UPDATE 1
```

再次查询：

```sql
postgres=# select * from books;
  id  |      name
------+-----------------
 1001 | PostgreSQL-15.2
(1 行记录)
```

输出信息：发现 name 值已经变成了 PostgreSQL-15.2，证明修改成功。



**删除 books 表行记录**，这是个人操作重要数据时有备份的习惯，开启显示事务，验证完后手动commit（提交）：

1. begin：手动开启显示事务。
2. delete：执行删除语句。
3. rollback：执行回滚操作。
4. commit：最后提交。

```sql
postgres=*# delete from books where id='1001';
DELETE 1
```

无论是 修改或者删除（统称更新操作），建议加上条件 where 语句。

无图无真相，如下所示为时间线操作步骤：

![](https://s1.ax1x.com/2023/04/25/p9KkC2F.png)



试一试 postgreSQL 使用 explain 分析SQL执行效率，和MySQL（MariaDB）差不多，参数显示更少：

```sql
postgres=# explain select * from books where id='1001'\g
                                QUERY PLAN
--------------------------------------------------------------------------
 Index Scan using books_pkey on books  (cost=0.14..8.16 rows=1 width=292)
   Index Cond: ((id)::text = '1001'::text)
(2 行记录)
```

因为创建表时，事先已经指定 id 属性为主键（primary key），所以执行计划扫描表使用到索引（using books_pkey）。 



**psql 帮助命令**：

1.   \? [commands] ：显示反斜线命令的帮助；
2.    \? options  ：显示 psql 命令行选项的帮助；
3.    \? variables  ： 显示特殊变量的帮助；
4.    \h [NAME]  ：  SQL命令语法上的说明，用*显示全部命令的语法说明。

最后，善用帮助文档，有助于你快速定位操作命令：

```bash
postgres=# \h
postgres=# \?
```
示例，我要查询alter具体用法：postgres-# \h alter 。如果你和我一样安装选择语言是中文版的rockyLinux，那么将有友好的中文翻译。

输出信息比较多：比如alter、create、drop等等DDL（Data Definition Language）语句。



**简单科普**：
DDL（Data Definition Language）语句，数据定义语句。主要用于对索引、数据表结构、字段等进行创建、删除以及修改。比如我们常用的关键字主要有：CREATE、DROP、ALTER等等。一般是DBA管理员使用的比较频繁。

DML（Data Manipulation Language）语句，数据操纵语句。主要用于对数据库表中记录进行增删改查。比如我们常用的关键字主要有：INSERT、DELTE、UPDATE以及SELECT等。一般是开发人员使用的比较频繁。

DCL（Data Control Language）语句，数据控制语句。主要用于对用户、表、字段的访问权限进行控制授权。比如我们常用的关键字有：grant（授权）、revoke（撤回授权）等。



退出 psql 终端管理命令： postgres=# \q

再次进入 psql 终端管理，执行：psql 



### 通用数据库管理软件 DBeaver

**初始化连接参数**：

1. 新增数据库连接，选择PostgreSQL。
2. 主机（host）：ip地址，localhost或者远程ip。
3. 数据库（database）：不填默认使用 postgres。
4. 端口（port）：默认为5432，实际工作中，建议修改，尽量避免被恶意扫描软件攻击。
5. 用户名（username）：初始化安装会存在一个超级用户 postgres。
6. 密码：可以使用 alter 语句修改，默认可能是空。

修改密码语句：

```sql
postgres=# ALTER USER postgres PASSWORD '123456';
```



![](https://s1.ax1x.com/2023/04/25/p9KFXbn.png)



**测试连接**，连接成功（正常）显示输出信息：

1. 选择顶部菜单栏：数据库。
2. 新建数据库连接。
3. 选择PostgreSQL，设置连接参数。
4. 测试连接。

![](https://s1.ax1x.com/2023/04/25/p9KFvEq.png)



**数据库目录导航，查询表 books**：

1. 定位数据库导航，选择postgres，依次展开public、表；
2. 右键（F4）查看表 books；
3. 选项：属性（显示表结构等等）、数据（行记录），ER图。

![](https://s1.ax1x.com/2023/04/25/p9KFLuj.png)



**使用SQL编辑器查询**：

1. 选择选择顶部菜单栏：SQL编辑器；
2. 新建SQL编辑器；
3. 输入SQL语句：select * from books b 。

![](https://s1.ax1x.com/2023/04/25/p9KFbvQ.png)



看完整篇教程后，有同学可能有疑问，你这张表的字段为什么这么少？没错，就是这么少。

初体验，第一次嘛，姿势动作难度不能太高，容易劝退，所以比较简单。创建用户、创建角色以及权限相关等等知识没有具体介绍，也许会在下一篇介绍哟。

至此，在 Linux 发行版 rockyLinux-9上初步体验 postgresql最新版本postgresql-15。



以上总结，仅供参考！

如需转载，请标明出处和原作者。



参考资料：

- PostgreSQL-15官方文档：[https://www.postgresql.org/docs/15/index.html](https://www.postgresql.org/docs/15/index.html)



—END—