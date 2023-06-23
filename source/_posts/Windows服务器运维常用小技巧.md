---
title: Windows服务器运维常用小技巧
date: 2022-02-18 
tags: Windows server
categories: 
- [开发运维]
---

Windows下常用的以及不常用的运维命令以及小技巧，看了绝对不会后悔。

总结：不难发现，很多Windows下的命令，基本上以.msc结尾，前缀是程序名称。比如磁盘管理命令：`diskmgmt.msc`


# 正文
## 一、远程桌面
快速进入远程桌面，主要是命令为`mstsc`

**方式一**：win + r打开运行输入`mstsc`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2382b87501614ca89f45bc888be647b7.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)


**方式二**：以管理员身份运行CMD输入以下命令：

```powershell
mstsc /v: 192.168.249.128 /console
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/089b96b94b7b496cbae7806733b36167.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)

## 二、win + r命令快速打开运行窗口
###  1、 win + r运行regedit：进入注册表
![在这里插入图片描述](https://img-blog.csdnimg.cn/e29e377dde74495ab590115dba60922e.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#p)
### 2、win + e：快速进入资源管理器
### 3、win + r运行入control：打开控制面板
![在这里插入图片描述](https://img-blog.csdnimg.cn/23f8a9f6f46b4d80ba9cf5c8d7c12b76.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)
### 4、win + r运行services.msc：进入服务管理
![在这里插入图片描述](https://img-blog.csdnimg.cn/095362cc626f499592020d8e7eedd29e.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)


### 5、运维使用小技巧
以下均为使用 **win + r** 快捷键打开运行如下命令：

**5.1、进入odbc配置**

```powershell
odbcad32
```

**5.2、进入磁盘清理**

```powershell
cleanmgr
```

**5.3、进入防火墙设置**

```powershell
WF.msc
```

**5.4、进入系统配置**

```powershell
#在安装Oracle11gR2卡在2%时会用到此命令快速进入配置调CPU核心数
msconfig
```
**5.4.1、进入系统配置，调CPU核心数**
![在这里插入图片描述](https://img-blog.csdnimg.cn/dce3209e7c144afe8c6edbf5945491c6.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)


**5.5、查看系统信息**

```powershell
msinfo32
```

**5.6、打开远程桌面**

```powershell
#这个命令上面也提到了，并做了详细截图
mstsc
```

## 三、查看系统的磁盘信息命令list disk
3.1、**win10自带的管理工具：diskpart.exe**

a、首先以管理员身份运行`CMD`
b、运行`diskpart`
c、运行`list disk`
![在这里插入图片描述](https://img-blog.csdnimg.cn/09ffbd9cf8084013a91f55ad4c665b9d.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)**3.2、进入磁盘管理命令**

```bash
#总结：不难发现，很多Windows下的命令，都是以.msc结尾，前缀这是程序名称。
win + r快捷键打开运行：diskmgmt.msc
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/d65c717857374809a901a97233b57a8c.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)

**3.3、进入计算机管理**

![在这里插入图片描述](https://img-blog.csdnimg.cn/540972f64863487e875b76e41bc5cce5.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)

```powershell
win + r运行：compmgmt.msc
```

**3.1.1、计算管理界面**，同理也能看到上面的磁盘管理
![在这里插入图片描述](https://img-blog.csdnimg.cn/210347e6e5cd4dba94229896be83b5b8.png?x-oss-process=,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RvbG92ZV9kcmVhbQ==,size_16,color_FFFFFF,t_70#)




## 四、netstat -ano
 单独拿出来讲，是因为netstat不仅仅在Linux下很实用，在Windows的DOS命令下一样很重要。

此命令主要用于查看占用的端口，通过管道符配合`findstr`命令缩小范围，类似于grep命令
```powershell
 netstat -ano | findstr /i  3306
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/5cd4d62dac444e27a11588d0f33a8928.png#)

## 五、tasklist命令
tasklist命令一般配合netstat命令使用（在windows下搭配使用很nice）
以达梦数据库和MySQL(MariaDB)数据库为例讲解

**查询达梦数据库的默认端口号5236，查出对应的PID号**
![在这里插入图片描述](https://img-blog.csdnimg.cn/d5a006aab45c4b2da68f85275872991f.png?x-oss-process=,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBA6b6Z6IW-5LiH6YeMc2t5,size_20,color_FFFFFF,t_70,g_se,x_16#)


```powershell
netstat -ano | grep 5236
```

配合tasklist定位进程名称

```powershell
tasklist | grep PID_PORT
```

查询MySQL(MariaDB)的默认端口号3306，查出对应的PID号

```powershell
netstat -ano | grep 3306
```

配合tasklist定位进程名称

```powershell
tasklist | grep PID_PORT
```


—END—

