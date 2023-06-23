---
title: Windows_server2012服务器部署Oracle11g：.NET和CPU核心数问题解决方案
date: 2021-10-09 
tags: Oracle
categories: 
- [数据库]
---

## 前言

主要以 Windows server2012R2 为主进行介绍，解决实际工作中遇到到的一些问题。

比如服务器 CPU 核心数过高，导致 Oracle 数据库安装时卡在 2% 的情况。

在 Windows 平台，你可以安装 VMware 工具模拟使用 Windows server 达到熟悉的目的。

![img](https://picx.zhimg.com/80/v2-fe5ce26ed9df00d5a05d2aa236cb91f0_720w.jpeg?source=d16d100b)



<!--more-->



说句心里话，我真没想到过我会在Windows服务器上总结这么多。一分耕耘一分收获，但是血赚不亏。

## 正文

第一次接触Windows服务器大约在5年前，那会的活动价我入手了入门级的Windows服务器。第一次安装了Windows server2012，低配版的服务器确实很吃力。


想熟悉Windows server服务器最新版，建议使用VMware配合服务器镜像。

**镜像获取地址**，推荐 [msdn，我告诉你](https://msdn.itellyou.cn/)。良心网站，专业收集原版镜像。


**关于想体验最新版的Windows11或者Windows server2022服务器**，可以访问新地址 [https://next.itellyou.cn/](https://next.itellyou.cn/)。

## 一、Oracle数据库安装开在2%

### 1、问题描述

1.1、**服务器CPU核心数过高**。在使用 Windows server2012 或者是其它 Windows 服务器，可能也会遇到这类问题。

### 2、解决问题

2.1、**解决问题，进入服务器的系统配置**，一次找到引导->高级选项，**设置处理器的核心数为16，然后重启即可生效**。

2.2、小技巧

**快捷键win + r，然后输入msconfig**命令即可快速进入系统配置。

![img](https://pic1.zhimg.com/80/v2-0ea42e97764352b980208b492cbf0645_720w.jpg?source=d16d100b)





## 二、安装.net3.5失败

### 1、准备工作，提取sxs

1.1、准备服务器镜像，可以**通过我上面提到的网址进行获取**。

![img](https://picx.zhimg.com/80/v2-ae35ab73de16263bce32c41625b60259_720w.png?source=d16d100b)




**1.2、提取sxs**

使用解压缩软件或者iso模拟软件打开镜像包，然后**进入/source/找到sxs**复制出来。在安装.net3.5时作为备用源使用，安装Oracle11gR2时需要安装.net3.5。

解压缩软件推荐360zip国际版（旧版1.0几的无广告）或者7z（体积小）。

![img](https://pic1.zhimg.com/80/v2-e952c64714b504b3455d1eb68b4ee687_720w.jpg?source=d16d100b)




### 2、再次安装.net3.5

### 2.1、指定依赖sxs，安装.net3.5

将之前从**Windows server中提取的sxs**复制到系统盘根目录下，然后在服务器仪表板中添加角色和功能（安装依赖），按照图上的提示**指定我们准备好的sxs源路径**，最终完美解决服务器上.net3.5无法安装的问题。

![img](https://pic1.zhimg.com/80/v2-ad95757957cdfb0499e6fd8b7f54ced5_720w.jpg?source=d16d100b)





### 2.2、Windows server仪表板

添加角色与功能，选择需要安装的功能时用得上，比如上面安装.net3.5

![img](https://picx.zhimg.com/80/v2-f46dcdbdfa18f66c41eccd296fda511c_720w.jpg?source=d16d100b)





## 三、操作小技巧

### 1、以Oracle服务为例

1.1、进入服务快捷命令，**win + r快捷键输入service.msc**，如下图所示

![img](https://pic1.zhimg.com/80/v2-39f6f46ab6b769eb86ef340e8c5dba2a_720w.png?source=d16d100b)




1.2、定位Oracle服务，你看到的Oracle服务是双倍的，因为我安装了双实例。实际工作中，并不推荐在单台服务器上部署双实例。不要问我为什么，因为实际中遇到过。内存也耗不起，最终把服务器拖挂掉了，最后通过清理日志解决。

![img](https://picx.zhimg.com/80/v2-c34e42b299d1a054b0a60e17f638d5f4_720w.jpg?source=d16d100b)




### 2、配置IP地址与DNS

配置IP地址与DNS与平时使用的win7或者win10是一样的配置方法

2.1、**进入控制面板找到网络和共享中心**

win + r 快捷键运行control命令进入控制面板，下图是VMware搭建的测试环境。

![img](https://picx.zhimg.com/80/v2-a5bc00f7ed3cce11c873923f78ad28f6_720w.jpg?source=d16d100b)




**2.2、配置IP地址和DNS**

![img](https://pica.zhimg.com/80/v2-d19089effc245b475e2fd96af6dbaeba_720w.jpg?source=d16d100b)




### 3、磁盘管理

最后再介绍一个小技巧，关于磁盘管理。当我们并不熟悉仪表板的操作时，或者旧版的服务器压根就没这玩意，如何处理。这是我们可以采用命令方式，先打开计算机管理。

同样使用win + r 快捷键，然后运行compmgmt.msc命令进入计算机管理，最后定位到磁盘管理。

![img](https://pic1.zhimg.com/80/v2-ff8ef218a407578907cdeb60580e459f_720w.jpg?source=d16d100b)




以上均为实际运维工作中使用到的小技巧，方便我们去管理维护服务器。在实际工作中，更多的是经验的累积。在之前的公司遇到这样一种，服务器的硬盘突然就gg思密达了。结果去查看后简直是让我措手不及，服务器版本那叫一个老，一些命令都不适用。心里真想来句mmp，最后还是硬着头皮上解决问题。

说实话，当时我在Windows服务器的实施与运维经验还没linux上丰富，现在想来完全是**工作让你不得不去适应**。


以上总结，仅供参考哟！如果你有幸看到本篇博文，希望对你的学习和工作有所帮助。

—END—