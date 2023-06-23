---
title: Windows与Linux安装JDK17
date: 2022-02-25 
tags: JDK
categories: 
- [开发工具]
---

**友情提醒**：当你看到本篇博文时，目前 JDK17 最新版已经更新到 JDK17.0.7。latest 代表最新版，当你点击如下给出的下载地址时，下载当前最新版本。

JDK 最新版 JDK17 下载与安装；Windows 版本与 Linux（ REHL 系列安装配置 JDK17），在 Windows 平台下 Eclipse ID E配置 JDK17。历史版本需要注册账号登录才能下载，真的太骚了，看着那个锁标志是锁住的。

前段时间，在某平台看到有人吐槽 CSDN 下载 JDK17 还需要付费。官方免费提供下载，CSDN欺负萌新不懂吗？

顺带一提目前使用比较广泛的两个 JDK 版本 JDK8 和 JDK11 最新版，需要登录账号才能下载哟：

1. JDK8最新版本：JDK8u321。
2. JDK11最新版本：JDK11.0.14。

在正式介绍 JDK 下载、安装、配置时，先来点科普知识。

1. JRE：Java 运行时环境（Java Runtime Environment），如果在非开发环境，只需运行，下载 JRE 即可。
2. JDK：Java 开发环境（Java Development Kit），通常包含 JDK 和 JRE ，某些新版本可能需要手动生成 JRE 。



Linux 平台 shell 环境变量调用顺序流程图：

![](https://s1.ax1x.com/2023/04/20/p9kLfrq.png)

<!-- more -->



# BEGIN JDK17下载与安装

## 一、JDK17下载地址

JDK官网提供三大平台下载地址：

1. Linux 版本 JDK 下载地址（ARM64和x64）。
2. macOS 版本 JDK 下载地址（ARM64和x64）。
3. Windows 版本 JDK 下载地址（x64）。



### 01 Windows 版本 JDK17

**tips**：图片资源可能被防盗链（寄）了，可以**右键属性复制地址在地址栏查看**哈。

> [https://www.oracle.com/java/technologies/downloads/#jdk17-windows](https://www.oracle.com/java/technologies/downloads/#jdk17-windows)

1. Compressed Archive：被压缩的归档包文件，其实是JDK归档压缩包，需要手动安装JRE。
2. x64 installer：x64架构exe安装包文件。
3. x64 msi installer：x64架构msi安装包文件。

![](https://img-blog.csdnimg.cn/img_convert/d94f4c4cc7463d16ef2b996f4c14f567.png)

**Windows版本zip压缩包JDK17.0.2下载地址**：

> [https://download.oracle.com/java/17/latest/jdk-17_windows-x64_bin.zip](https://download.oracle.com/java/17/latest/jdk-17_windows-x64_bin.zip)

Windows版本x64安装包exe文件安装包文件JDK17下载地址：

> [https://download.oracle.com/java/17/latest/jdk-17_windows-x64_bin.exe](https://download.oracle.com/java/17/latest/jdk-17_windows-x64_bin.exe)

Windows版本x64安装包msi安装包文件JDK17下载地址：

> [https://download.oracle.com/java/17/latest/jdk-17_windows-x64_bin.msi](https://download.oracle.com/java/17/latest/jdk-17_windows-x64_bin.msi)



### 02 Linux 版本 JDK17

Linux版JDK17.0.2下载：分为ARM64和x64架构

1. ARM64 Compressed Archive：被压缩的归档包文件，其实是JDK归档压缩包。
2. ARM64 RPM Packages：ARM64架构rpm包。
3. **x64 Compressed Archive**：被压缩的归档包文件，其实是JDK归档压缩包，编译后的二进制包。
4. x64 Debian Packages：x64架构deb包，在某版本之后同样适用于Ubuntu系列、中标麒麟以及银河麒麟。
5. x64 RPM Packages：x64架构rpm包。

> [https://www.oracle.com/java/technologies/downloads/#jdk17-linux](https://www.oracle.com/java/technologies/downloads/#jdk17-linux)

![](https://img-blog.csdnimg.cn/img_convert/1e54cdae9e37be028d8526de78baecdd.png)

JDK 二进制包下载地址：

> [https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.tar.gz](https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.tar.gz)



### 03 MacOS 版本 JDK17

MAC版本JDK17下载地址：

> [https://www.oracle.com/java/technologies/downloads/#jdk17-mac](https://www.oracle.com/java/technologies/downloads/#jdk17-mac)

![](https://img-blog.csdnimg.cn/img_convert/3a7e6ab587c3c985eb2cfb96a30d32ce.png)



## 二、Windows 安装 JDK17（Archive）

介绍zip包的使用，不用点那个烦人的下一步下一步，比较自由，得自己控制。

**注意**：有可能存在配置环境变量后没有及时生效，重启就好了。



### 01 zip 包 JDK 手动安装 JRE

当然我自己也做了测试，对于`jdk12`、`jdk14`、`jdk17`都适用。其它版本，没测试过。

1. 切换至jdk解压目录：D:\work\JavaEE\jdk17.0.2
2. 查看当前JDK版本，切换至jdk17.0.2\bin目录执行：`java -version`，看下面代码示例就很清晰。
3. 执行命令：bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre，**注意我执行命令的目录**。

```bash
cd D:\work\JavaEE\jdk17.0.2\bin
#1.查看jdk版本
java -version
java version "17.0.2" 2022-01-18 LTS
Java(TM) SE Runtime Environment (build 17.0.2+8-LTS-86)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.2+8-LTS-86, mixed mode, sharing)
#2.生成jre,注意我执行命令的目录
D:\work\JavaEE\jdk17.0.2>bin\jlink.exe --module-path jmods --add-modules java.desktop --output jre
```



### 02 Eclipse IDE 添加 JDK17

1. 找到Eclipse IDE状态栏的Windows选项。
2. 点击Windows然后打开Preferences。
3. 搜索`jres`，选中`Installed JREs`，点击右侧add添加JDK17。
4. 添加完JDK选apply and close：应用并退出。

Eclipse IDE添加JDK17第一步：**选择Add添加**

![](https://img-blog.csdnimg.cn/img_convert/46b3699e169fe1969bbb836c9623ea65.png)



Eclipse IDE添加JDK17第二步：**选择VM点击next进行下一步**

![](https://img-blog.csdnimg.cn/img_convert/635f7e2f692034c543bd8959a98b44d5.png)



Eclipse IDE添加JDK17第三步：**选择Directory添加JDK安装目录，然后点击finish完成**。



 ![](https://img-blog.csdnimg.cn/img_convert/742e118c4bd9868301426dce8a6fc3c2.png)



**完成添加JDK17，点击apply and close应用并提出当前窗口**：

![](https://img-blog.csdnimg.cn/img_convert/9ba43cb7f475baced5318fdc9d1fd3a5.png)



### 03 Windows 下配置 JDK 环境变量

根据自己需求来，为了方便，建议配置一个经常使用的版本作为当前用户或者全局环境变量。

在实际工作中，我可以有多种方式去给自己测试的web应用配置JDK，一般情况是**startup.bat或者catalina.bat**文件中指定，**比如tomcat中指定JDK目录**，或者在rocketmq中也可以指定JDK目录：

```bash
JAVA_HOME=D:\work\JavaEE\jdk17.0.2
```

**开始配置环境变量**：

1. 编辑当前用户或者系统环境变量加入如下配置：D:\work\JavaEE\jdk17.0.2
2. 编辑当前用户或者系统PATH环境变量加入如下配置：D:\work\JavaEE\jdk17.0.2\bin
3. 编辑当前用户或者系统CLASS_PATH环境变量加入如下配置：`.;%JAVA_HOME%\bin;%JAVA_HOME%\lib\dt.jar;%Java_Home%\lib\tools.jar;%SystemRoot%/system32;%SystemRoot%;`，**注意结尾英文分号隔开**，在JDK5以后是可以不用配置这一选项。

编辑当前用户或者系统环境变量：**添加JAVA_HOME**

![](https://img-blog.csdnimg.cn/img_convert/dcddc9686691b52695804d069ca4dd95.png)

```bash
变量名:JAVA_HOME
变量值:D:\work\JavaEE\jdk17.0.2
```

配置 JAVA_HOME 后的效果：

![](https://img-blog.csdnimg.cn/img_convert/4ebf346824c82027d374dbdca36f5948.png)

编辑当前用户或者系统环境变量：**添加PATH**

![](https://img-blog.csdnimg.cn/img_convert/8fa361711ae04248141699459c73d076.png)

```bash
变量名: PATH
变量值: D:\work\JavaEE\jdk17.0.2\bin 
或者配合成: %JAVA_HOME%
```

**添加后的path环境变量**，个人测试配置了很多，其实大部分是系统自动生成的：

![](https://img-blog.csdnimg.cn/img_convert/7154927140f25deec45a18a4233985da.png)

编辑当前用户或者系统环境变量：**添加CLASS_PATH**

```bash
变量名:CLASS_PATH
变量值:.;%JAVA_HOME%\bin;%JAVA_HOME%\lib\dt.jar;%Java_Home%\lib\tools.jar;%SystemRoot%/system32;%SystemRoot%;
```



## 三、Linux（REHL系列）安装 JDK17

Linux 平台 shell 环境变量调用顺序流程图：

![](https://s1.ax1x.com/2023/04/20/p9kLfrq.png)



安利一款实用多终端管理工具tabby，其实也不用我安利，在github上已经快30K的star（星标）。最新版可以设置中文模式。当我更新到 Windows 11 后，自带的 Windows terminal 也可以满足一般需求，挺好用的。



![](https://img-blog.csdnimg.cn/img_convert/c1cea421255b93fc526c8a061b1e2ced.png)



如同 Windows 平台配置环境变量一样，Linux 平台也有当前用户和全局用户（root）环境变量两种配置方式。

以下均作为演示，仅供参考，不喜勿喷。



### 01 Linux（REHL系列）安装 JDK17

1. 解压jdk17安装包

```bash
[root@cnwangk work]# tar -zxvf jdk-17_linux-x64_bin.tar.gz
```

2. 修改名称为jdk17，为后面配置环境变量JAVA_HOM做准备

```bash
[root@cnwangk work]# mv jdk-17.0.2 jdk17 
```

3. 剪切jdk17到其它目录方便自己管理

```bash
[root@cnwangk work]# mv jdk17/ /usr/local/
```

4. 查看JDK版本，在没配置JAVA_HOME环境变量之前一样可以查看版本

```bash
[root@cnwangk bin]# ls
jar        javac    jcmd      jdeprscan  jhsdb   jlink  jpackage    jshell  jstatd       serialver
jarsigner  javadoc  jconsole  jdeps      jimage  jmap   jps         jstack  keytool
java       javap    jdb       jfr        jinfo   jmod   jrunscript  jstat   rmiregistry
[root@cnwangk bin]# ./java -version
java version "17.0.2" 2022-01-18 LTS
Java(TM) SE Runtime Environment (build 17.0.2+8-LTS-86)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.2+8-LTS-86, mixed mode, sharing)
```

5. 安装JRE，主要是利用`jlink`去生成，在解压后jdk17的bin目录下

```bash
[root@cnwangk jdk17]# ./bin/jlink --module-path jmods --add-modules java.desktop --output jre
[root@cnwangk jdk17]# ls
bin  conf  include  jmods  jre  legal  lib  LICENSE  man  README  release
```

能贴代码做演示的，我一般不愿意贴图，因为图片可能会因为各种原因挂掉。



### 02 Linux（REHL系列）配置 JDK 环境变量

如果想环境变量即时生效，执行 `source /etc/profile`  命令即可。

1. 全局环境变量，**需要root用户权限**
2. 编辑`profile`文件：`vim /etc/profile`，加入如下配置：

![](https://img-blog.csdnimg.cn/img_convert/146ce95aa5e8e98fbe77e86d6f36b872.png)

```bash
#JAVA environment
JAVA_HOME=/usr/local/jdk17
PATH=$PATH:$JAVA_HOME/bin
export JAVA_HOME PATH
```

3. 配置jdk环境变量在当前用户test生效
4. 编辑`.bash_profile`文件：`vim /home/test/.bash_profile`
5. 在`.bashrc`和`.bash_profile`都有可以看到环境变量，个人一般编辑.bash_profile

![](https://img-blog.csdnimg.cn/img_convert/acb1355ed068ce1f592ba3330f714da7.png)

```bash
#JAVA environment
JAVA_HOME=/usr/local/jdk17
PATH=$PATH:$JAVA_HOME/bin
export JAVA_HOME PATH
```

6. **因为上面配置了全局的**，所以我在test用户下一样可以查看jdk版本

```bash
[test@cnwangk jdk17]$ java -version
java version "17.0.2" 2022-01-18 LTS
Java(TM) SE Runtime Environment (build 17.0.2+8-LTS-86)
Java HotSpot(TM) 64-Bit Server VM (build 17.0.2+8-LTS-86, mixed mode, sharing)
```


Linux 环境变量**立即生效**两种方式：

- 使用source命令：`source /etc/profile`
- 重启服务器：`reboot` 或者 `shutdown -r now`



关于JDK17的下载与安装就介绍到这里。

# END 向阳而生

向阳而生，生而向阳。

静下来心才好做事，思路更清晰。每天进步一点，进步一小点那也是进步。

引用晚清中兴第一名臣，曾国藩家训中的一句名言，颇为受用：

> 养得胸中一种恬静。



以上总结，仅供参考哟！希望对你的学习和工作有所帮助。

——END——
