---
title: Linux-CentOS-Stream-9使用htop命令监控服务器
date: 2023-04-03 22:34:01
tags: htop
categories: 
- [开发运维]
---


**使用 htop -t 效果展示如下图**：

![pp49tOO.png](https://s1.ax1x.com/2023/04/03/pp49tOO.png)



htop 支持Linux发行版比较丰富，以RHEL9（EL9）CentOS Stream 9进行示例演示。



**htop仓库地址**：https://github.com/htop-dev/htop

htop官网：https://htop.dev/downloads.html

epel：https://docs.fedoraproject.org/en-US/epel/



**RHEL使用epel库，CentOS Stream 9**：

```bash
dnf config-manager --set-enabled crb
dnf install epel-release epel-next-release
```



wget获取epel：

```bash
wget https://dl.fedoraproject.org/pub/epel/epel-next-release-latest-9.noarch.rpm
```



**epel依赖库安装**：

```bash
rpm -ivh epel-next-release-latest-9.noarch.rpm
```

**htop安装**：

```bash
dnf -y install htop
```

htop 查看当前版本：
```bash
htop -V
htop 3.2.2
```

**htop 运行**：

```bash
htop
htop -t
```
参数 -t ：Tree，显示目录树结构。



htop 帮助文档：

```bash
htop -h 
htop --help
```

