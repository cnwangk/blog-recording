---
title: Linux服务器挂载硬盘详细教程
date: 2021-09-09
tags: Linux
categories: 
- [开发运维]
---

Linux服务器挂载硬盘详细教程。


# 前言
本文将带来linux下的磁盘管理中的硬盘挂载，Linux操作系统挂载硬盘需要了解的一些知识。这可能是迄今为止介绍的最最最实用的linux硬盘挂载的文章了，比较详细。由于工作原因，平时使用的比较多。主要目的，只是想让更多人的了解到linux下挂载磁盘也不是那么困难。

有几种常见的文件系统，以前的老牌文件系统ext文件系统(ext2、ext3、ext4)。

在Redhat7系列还是推荐一款优秀的xfs文件系统，在性能上已经超越了ext文件系统。XFS文件系统是硅谷图形公司（Silicon Graphic Inc，简称SGI）开发的用于IRIX（一个Unix操作系统）的文件系统，后来将其移植到Linux操作系统上。XFS是一个高级日志文件系统，其优势是极具伸缩性，同样也极具健壮性。

还有一款btrfs（B-tree文件系统通常读作Buffer FS、Better FS、B-tree FS）文件系统同样很优秀，Redhat7安装就自带。
btrfs具有很多特性。例如：写快照、快照的快照、内建RAID（通常称为磁盘阵列）、子卷（subvolume），其最核心的理念是设计
容错、修复以及易于管理。btrfs最大容量卷为16EB，单个最大文件为16EB。

须知：本文全程使用的是安装选择语言是简体中文版的，所以看到的汉字显示，请不要惊讶。

![](https://img-blog.csdnimg.cn/img_convert/5324a76fbd054b60d2769434dc9ef136.png)

# 正文

开局一张图，文章全靠编。开个玩笑，纯属逗大家乐一乐。下面的图片，已经点明了本文的核心内容。

![](https://img-blog.csdnimg.cn/img_convert/06ab3c857d7db1c575a69bc7a1e2ab3c.png)

**建议：进行测试，可以使用虚拟机配合linux（Redhat系列或者Ubuntu搭建环境）测试**。

## 一、查看系统分区情况
fdisk参数说明
删除存在的硬盘分区，此时会提示需要删除的序列号是哪一个。

- 删除分区：d

- 新增分区：n
- 查看分区信息：p
- 保存分区变更信息：w
- 不保存并退出：q
- 获取帮助信息：m

### 1、列出分区表

列出分区表，从下面的列出的选项可以看出，原始的磁盘磁盘 /dev/sda：21.5 GB是初始安装linux操作系统就分配的。另外一块磁盘，是我新增的磁盘sdb用于测试演示。

```bash
fidsk -l
[root@cnwangk /]# fdisk -l

磁盘 /dev/sda：21.5 GB, 21474836480 字节，41943040 个扇区
Units = 扇区 of 1 * 512 = 512 bytes
扇区大小(逻辑/物理)：512 字节 / 512 字节
I/O 大小(最小/最佳)：512 字节 / 512 字节
磁盘标签类型：dos
磁盘标识符：0x0001805e

   设备 Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048      411647      204800   83  Linux
/dev/sda2          411648     4507647     2048000   83  Linux
/dev/sda3         4507648     8603647     2048000   82  Linux swap / Solaris
/dev/sda4         8603648    41943039    16669696    5  Extended
/dev/sda5         8605696    41943039    16668672   83  Linux

磁盘 /dev/sdb：10.7 GB, 10737418240 字节，20971520 个扇区
Units = 扇区 of 1 * 512 = 512 bytes
扇区大小(逻辑/物理)：512 字节 / 512 字节
I/O 大小(最小/最佳)：512 字节 / 512 字节
磁盘标签类型：dos
磁盘标识符：0x95df3b22

   设备 Boot      Start         End      Blocks   Id  System
/dev/sdb2        10485760    20971519     5242880   83  Linux
```

直接输入fdisk命令，中文版会提示帮助信息以及使用方法

```bash
fdisk [选项] <磁盘>    更改分区表
#例如新增的磁盘sdb
fdisk /dev/sdb
fdisk [选项] -l <磁盘> 列出分区表
fdisk -s <分区>        给出分区大小(块数)
```



## 二、建立linux文件系统

### 1、xfs文件系统

如下所示，我将新建xfs文件系统，指向的是新增的一块磁盘文件路径/dev/sdb。同样也是Redhat7系列默认推荐的使用格式。

```bash
mkfs.xfs  /dev/sdb 
```

做一个简单说明：xfs文件系统提供了备份分区工具xfsdump以供用户使用。优势在于用户不用借助第三方软件就可以实现对xfs文件系统上的数据实施备份。备份过程如下所示：

```bash
xfsdump /backup/dump_sdc1 /sdc1
```

### 2、btrfs文件系统

如下所示，我将新建btrfs文件系统，指向的是新增的一块磁盘文件路径/dev/sdb，下面最终演示的也是btrfs文件系统的配置。

```bash
mkfs.btrfs /dev/sdb
```

### 3、ext文件系统

在Redhat6以及之前，用的还是ext文件系统。后来到7系列推荐使用xfs文件系。

```bash
mkfs.ext4 /dev/sdb
```



## 三、创建要挂载的路径

### 1、创建挂载的文件data

使用mkdir命令创建data目录，用于后续挂载新增的磁盘。

```bash
mkdir /data
```

查看创建好的挂载路径data，初始是空的

```bash
ls /data
```

### 2、使用磁盘

写入一个简单`shell`的脚本作为演示

```bash
echo -e "echo "hello linux"\necho "create btrfs filesystem"" >> /data/data.sh
```

写入简单的shell脚本后，测试查看并执行这个脚本

```bash
#再次查看data盘下的文件
[root@cnwangk /]# ls /data/
data.sh
sh /data/data.sh
#运行脚本
[root@cnwangk /]# sh /data/data.sh 
hello linux
create btrfs filesystem
```

从上面可以看出一个基本的磁盘的管理，会引出一些基本命令的使用，比如ls、mkdir、echo等等。本文的受众群体是需要掌握一些linux基本命令知识的。当然能看到本文的，也说明您还是有一些基础的。



## 四、使用fdisk对/dev/sdb进行分区

### 1、分区命令fdisk

使用fdisk对新增的磁盘/dev/sdb进行分区，之前演示我已经使用主分区2，现在演示是逻辑扩展分区，使用参数e。

- 新增分区：n
- 新增主分区：p
- 扩展分区：e
- 注意：你可以自定义大小，也可以回车就是使用默认大小和扇区。

```bash
fdisk /dev/sdb
[root@cnwangk /]# fdisk /dev/sdb
欢迎使用 fdisk (util-linux 2.23.2)。

更改将停留在内存中，直到您决定将更改写入磁盘。
使用写入命令前请三思。

命令(输入 m 获取帮助)：n #新增分区，p则为主分区，e则为扩展分区
Partition type:
   p   primary (1 primary, 0 extended, 3 free)
   e   extended
Select (default p): e
分区号 (1,3,4，默认 1)：1
起始 扇区 (2048-20971519，默认为 2048)：
将使用默认值 2048
Last 扇区, +扇区 or +size{K,M,G} (2048-10485759，默认为 10485759)：
将使用默认值 10485759
分区 1 已设置为 Extended 类型，大小设为 5 GiB

命令(输入 m 获取帮助)：p #此时用参数p查看未保存的分区信息

磁盘 /dev/sdb：10.7 GB, 10737418240 字节，20971520 个扇区
Units = 扇区 of 1 * 512 = 512 bytes
扇区大小(逻辑/物理)：512 字节 / 512 字节
I/O 大小(最小/最佳)：512 字节 / 512 字节
磁盘标签类型：dos
磁盘标识符：0x95df3b22
#查看到新增分区的设备信息
   设备 Boot      Start         End      Blocks   Id  System
/dev/sdb1            2048    10485759     5241856    5  Extended
/dev/sdb2        10485760    20971519     5242880   83  Linux

命令(输入 m 获取帮助)：w #输入w参数进行保存，输入q进行不保存退出。
The partition table has been altered!

Calling ioctl() to re-read partition table.

WARNING: Re-reading the partition table failed with error 16: 设备或资源忙.
The kernel still uses the old table. The new table will be used at
the next reboot or after you run partprobe(8) or kpartx(8)
正在同步磁盘。
```



## 五、建立btrfs文件系统

### 1、建立文件系统

新建btrfs文件系统，在确定进行分区之后执行此命令，最后进行挂载磁盘。

```bash
mkfs.btrfs /dev/sdb2
```

同样可以使用如下命令

```bash
mkfs -t btrfs /dev/sdb2
```



## 六、挂载文件系统

### 1、挂载命令mount

接着上面建立好`btrfs`文件系统，此时再挂载到新建的data目录下。**虽然是挂载成功了，但只是临时生效，重启会掉盘挂载后硬盘。而且卷标还会显示成字母加数字的一串长字符串，类似这种s1k544y55fsa445dda44sd4545eff4字符串**。究其原因，Linux还是以文件系统为核心的。没有目录这个概念，只是方便大家理解，都习惯这样称呼。

1.1、使用`mount`挂载，看到的是sdb2，是因为之前已经创建了一个分区sdb1。

```bash
mount /dev/sdb2 /data
```

1.2、使用umount卸载

```bash
umount /dev/sdb2 /data
```



### 2、写入fstab文件

2.1、**永久生效需要写入/etc/fstab文件**中，使用`echo`命令追加数据到fstab文件中。

```bash
#第一项参数/dev/sdb这里也可以写入UUID的信息
#	 第一项参数	 第二项参数	  第三项参数		第四项参数	第五项参数
echo /dev/sdb1    /data   	  btrfs    	  defaults     0 0  	>>  /etc/fstab
echo /dev/sdb2    /data   	  btrfs    	  defaults     0 0  	>>  /etc/fstab
```

2.2、输入`blkid`命令查看卷标或者UUID

```bash
# blkid命令
[root@cnwangk /]# blkid
/dev/sda5: UUID="d4708f44-beed-4a9b-bb11-94706e6c0cf5" TYPE="xfs" 
/dev/sda1: UUID="7d56f743-a42d-42e2-876e-d839cc583fa7" TYPE="xfs" 
/dev/sda2: UUID="953b1070-a13a-4b67-ac63-cc376c1dee8d" TYPE="xfs" 
/dev/sda3: UUID="b075b6d0-4d37-4f18-ae59-bf380862b440" TYPE="swap" 
/dev/sdb2: UUID="294c0c25-04be-4791-ab06-520c4283cb58" UUID_SUB="a8b7194a-a694-4a8a-bee1-0ab49821e6bb" TYPE="btrfs" 
```

2.3、当然，你可以**使用btrfs自带的命令查看磁盘文件的uuid**

```bash
[root@cnwangk /]# btrfs filesystem show
Label: none  uuid: 294c0c25-04be-4791-ab06-520c4283cb58
        Total devices 1 FS bytes used 192.00KiB
        devid    1 size 5.00GiB used 536.00MiB path /dev/sdb2
```



## 七、永久写入配置文件

### 1、配置文件fstab展示

注意：解决重启掉盘的问题。强调一点，**一旦写入配置文件的参数出现错误异常，大概率导致服务器无法启动，所以修改时需谨慎操作**。最好先做备份，再进行操作。

如下我的`/ect/fstab`配置文件内容，可以看到`/dev/sdb2`是我测试新增的一块盘进行分区后的配置，使用文件系统格式为`btrfs`。

```bash
# /etc/fstab
# Created by anaconda on Sun Jan  5 21:10:23 2020
#
# Accessible filesystems, by reference, are maintained under '/dev/disk'
# See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
#
UUID=d4708f44-beed-4a9b-bb11-94706e6c0cf5 /                       xfs     defaults        0 0
UUID=7d56f743-a42d-42e2-876e-d839cc583fa7 /boot                   xfs     defaults        0 0
UUID=953b1070-a13a-4b67-ac63-cc376c1dee8d /home                   xfs     defaults        0 0
UUID=b075b6d0-4d37-4f18-ae59-bf380862b440 swap                    swap    defaults        0 0
/dev/sdb2                                /data                    btrfs   defaults        0 0
```



### 2、部分参数详解

写入卷标信息到`/etc/fstab`文件（**Redhat7系列默认推荐格式为xfs**，从我文中给出的展示就可看出）

- 第一项参数：/dev/sdb1（原始磁盘分区路径）
- 第二项参数：/data（新建的挂载磁盘文件路径，Linux核心是一个文件系统，所以说是文件路径）
- 第三项参数：btrfs（挂载磁盘文件系统格式）
- 第四项参数：defaults
- 第五项参数：0 0

```bash
#第一项参数/dev/sdb这里也可以写入UUID的信息
#	 第一项参数	 第二项参数	  第三项参数		第四项参数	第五项参数
echo /dev/sdb1    /data   	  btrfs    	  defaults     0 0  	>>  /etc/fstab
```

### 3、修改配置文件

可以直接编辑文件新增磁盘挂载信息：`vim /etc/fstab`
写入到`/etc/fstab`配置文件，文件系统推荐xfs或者btrfs，具体视实际情况而定：

```bash
/dev/sdb2    /data     ext4    defaults    0 0
/dev/sdb2    /data     xfs     defaults    0 0
/dev/sdb2    /data     btrfs   defaults    0 0
```

**重启生效**：`reboot`  或者 `shutdown -r now`

**验证挂载是否成功**，此时重启系统后可以看到我的新挂载的磁盘/dev/sdb2已经生效了并写入了fstab配置文件。

```bash
df -h
[root@cnwangk /]# df -h
文件系统        容量  已用  可用 已用% 挂载点
devtmpfs        907M     0  907M    0% /dev
tmpfs           917M     0  917M    0% /dev/shm
tmpfs           917M  9.3M  908M    2% /run
tmpfs           917M     0  917M    0% /sys/fs/cgroup
/dev/sda5        16G  7.1G  8.9G   45% /
/dev/sdb2       5.0G   17M  4.5G    1% /data
/dev/sda2       2.0G   34M  2.0G    2% /home
/dev/sda1       197M  154M   43M   79% /boot
tmpfs           184M     0  184M    0% /run/user/0
```





## 八、磁盘管理

其实，上面对硬盘进行分区已经使用到了磁盘管理命令格式化分区`mkfs`、分区`fdisk`，属于基本的磁盘管理。还有最常用的`df`，用来查看磁盘空间占用情况；`mount`与`umount`命令进行挂载与卸载磁盘。主要想引出的是如下的第三方ssm管理工具。

看到这个ssm不要与Javaweb中的框架组合ssm（Spring Springmvc Mybatis）混淆了。

### 1、ssm管理工具

ssm（System Storage Manager）管理逻辑卷。默认没有安装，需要手动安装，下载rpm包或者直接yum源在线安装都行：

```bash
#提供yum在线安装方式
yum -y install system-storage-manager.noarch
```

安装完后，如下**使用ssm命令**即可展示效果：

```bash
[root@cnwangk /]# ssm list
-----------------------------------------------------------------
Device        Free       Used      Total  Pool        Mount point
-----------------------------------------------------------------
/dev/fd0                         4.00 KB                         
/dev/sda                        20.00 GB                         
/dev/sda1                      200.00 MB              /boot      
/dev/sda2                        1.95 GB              /home      
/dev/sda3                        1.95 GB              SWAP       
/dev/sda4                        1.00 KB                         
/dev/sda5                       15.90 GB              /          
/dev/sdb                        10.00 GB                         
/dev/sdb1                        1.00 MB                         
/dev/sdb2  4.48 GB  536.00 MB    5.00 GB  btrfs_sdb2             
-----------------------------------------------------------------
-----------------------------------------------------
Pool        Type   Devices     Free     Used    Total  
-----------------------------------------------------
btrfs_sdb2  btrfs  1        5.00 GB  5.00 GB  5.00 GB  
-----------------------------------------------------
-----------------------------------------------------------------------------------
Volume      Pool        Volume size  FS       FS size      Free  Type   Mount point
-----------------------------------------------------------------------------------
btrfs_sdb2  btrfs_sdb2      5.00 GB  btrfs    5.00 GB   5.00 GB  btrfs  /data      
/dev/sda1                 200.00 MB  xfs    196.66 MB  42.79 MB         /boot      
/dev/sda2                   1.95 GB  xfs      1.94 GB   1.91 GB         /home      
/dev/sda5                  15.90 GB  xfs     15.89 GB   8.87 GB         /          
-----------------------------------------------------------------------------------
```



### 2、linux自带的磁盘命令

比如，查看磁盘空间状态，加上参数-h以（K、M、G）形式显示。虽然df可以以多种形式展示，但个人工作中最常用的，还是加上-h参数使用的最为频繁。下面以加上参数-h为例子进行展示：

```bash
df -h
[root@cnwangk /]# df -h
文件系统        容量  已用  可用 已用% 挂载点
devtmpfs        907M     0  907M    0% /dev
tmpfs           917M     0  917M    0% /dev/shm
tmpfs           917M  9.3M  908M    2% /run
tmpfs           917M     0  917M    0% /sys/fs/cgroup
/dev/sda5        16G  7.1G  8.9G   45% /
/dev/sdb2       5.0G   17M  4.5G    1% /data
/dev/sda2       2.0G   34M  2.0G    2% /home
/dev/sda1       197M  154M   43M   79% /boot
tmpfs           184M     0  184M    0% /run/user/0
```

在df命令后加上-a参数，显示所有文件系统磁盘使用情况，这里就不贴输出的内容了，显示内容太长了。

```bash
df -ah
```

**以上就是此次文章的所有内容的，希望能对你的工作有所帮助。感觉写的好，就拿出你的一键三连。如果感觉总结的不到位，也希望能留下您宝贵的意见，我会在文章中进行调整优化。**

**原创不易，转载也请标明出处，本文会不定期上传到gitee或者github以及VX公众平台。**

最后给出思维导图，凑合着看看吧，权当有个印象！

![](https://img-blog.csdnimg.cn/img_convert/7a9b5700ab6514c606462bee53c1d837.png)

