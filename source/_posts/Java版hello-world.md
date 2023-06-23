---
title: 程序人生：人生中的第一个 Java 应用程序 hello world
date: 2017-01-01 
tags: Java
categories: 
- [web开发]
---

算是开个人 blog 第一篇博文。

程序人生：人生中的第一个Java应用程序 hello java！

开局一张图，程序全靠编：

![](https://s1.ax1x.com/2023/05/15/p92J3q0.png)



<!-- more -->

### Hello Java



**准备环境**

- JDK
- STS4（Spring Tool Suit4）



**安装JDK17**
Windows平台：

```bash
unzip jdk-17.0.4.1_windows-x64_bin.zip
mv jdk-17.0.4.1 jdk17
```
加入环境变量：
1. win + x + y：找到高级系统设置
2. 编辑用户环境变量：新增 JAVA_HOME 引入 JDK 安装目录，例如：D:\jdk17
3. 编辑用户环境变量：找到 Path 加入 %JAVA_HOME%;


Linux平台：
```bash
tar -zxvf jdk-17.0.4.1_linux-x64_bin.tar.gz
mv jdk-17.0.4.1 jdk17
mkdir -p /usr/java
mv jdk17  /usr/java/
```

加入环境变量：sudo vim /etc/profile
```bash
# JAVA ENV
JAVA_HOME=/usr/java/jdk17
CLASS_PATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
PATH=$PATH:$JAVA_HOME/bin
export JAVA_HOME CLASS_PATH PATH
```

即时生效，执行 source 命令：

```bash
source /etc/profile
```





**验证版本**

```bash
java -version
```



**编写Java类**
如果有 vi  &  vim 环境（通常Linux发行版自带）：vim Test.java

桌面环境（无IDE）：使用编辑器编辑（记事本  sublime text  VSCode）新建文件：Test.java

桌面环境（有IDE）：Eclipse for JavaEE、STS4（SpringToolSuit4）、IntelliJ 
IDEA 或者 VSCode（安装 SpringToolSuit4 插件）任选一款构建 Java Project：Helloworld，然后 New、选 Class，新增文件：Test.java

结构清单：
- Helloworld
	+ src
		* （default package）Test.java


输入如下内容：
```java
public class Test {
	public static void main(String[] args) {
		helloWorld();
	}

	public static void helloWorld(){
		String hello_world ="hello world";
		System.out.println(hello_world);
	}
}
```



**Run：运行**

输入：

```bash
java Test.java
```
**注意**：某些低版本JDK需要先执行javac Test.java，再执行 java Test

输出：hello world



### 骚操作

开局图片效果，是如下示例输出结果。

**Rocky 9 Linux**

**输入**如下内容，Linux 平台终端使用 vim 编辑时，打印输出需要注意圆点和引号的转义：

vim Test.java

```java
class Test{
        public static void main(String args[]){
                System.out.println("佛祖保佑！！！");
                  System.out.println("////////////////////////////////////////////////////////////////////");
 System.out.println("//                          _ooOoo_                               //");
 System.out.println("//                         o8888888o                              //");
 System.out.println("//                         88\" . \"88                              //");
 System.out.println("//                         (| ^_^ |)                              //");
 System.out.println("//                         O\\  =  /O                              //");
 System.out.println("//                      ___//`---'\\____                           //");
 System.out.println("//                    .'  \\|     |//  `.                          //");
 System.out.println("//                   /  \\|||  :  |||//  \\                         //");
 System.out.println("//                  /  _||||| -:- |||||-  \\                       //");
 System.out.println("//                  |   | \\\\  -  /// |    |                       //");
 System.out.println("//                  | \\_|  ''\\---//''  |   |                      //");
 System.out.println("//                  \\  .-\\__  `-`  ___//-. //                     //");
 System.out.println("//                ___`. .'  /--.--\\  `. . ___                     //");
 System.out.println("//            .\"\" '<  `.___\\_<|>_//___.'  >'\"\".                   //");
 System.out.println("//            | | :  `- \\`.;`\\ _ //`;.`/ - ` : | |                //");
 System.out.println("//            \\  \\ `-.   \\_ __\\ //__ _/   .-` /  /                //");
 System.out.println("//      ========`-.____`-.___\\_____/___.-`____.-'========         //");
 System.out.println("//                           `=---='                              //");
 System.out.println("//      ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^        //");
 System.out.println("//      佛祖保佑       永无BUG     永不修改        永不宕机       //");
 System.out.println("////////////////////////////////////////////////////////////////////");
            
            System.out.println("永不宕机！！！");
        }
}
```


**Windows 平台**
如果，你有 vim 环境，同样可以在 CMD 字符命令环境或者 PowerShell 环境使用 vim 编辑 Test.java。

好吧，我想大抵是没有安装的。

使用 Windows 平台自带的记事本或者下载第三方编辑器，新建 Test.java，然后编辑并输入上面的演示内容。


**Run 运行**

```bash
java Test.java
```

**输出**结果，开局一张图。



示例，玩笑话，就当乐呵呵。

写代码，无法做到永无 bug ；服务器，也无法做到永不宕机。

人生也一样，终身有忧处，终身有乐处。



以上总结，仅供入门参考哟！

—END—



