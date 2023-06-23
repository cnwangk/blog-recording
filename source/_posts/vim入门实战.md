---
title: vim入门实战
date: 2023-02-26 20:04:54
tags: vim
categories: 
- [开发工具]
---

一入编程深似海，从此节操是路人。

**前段时间由于业务场景需求**，不得不近一步学习 vim 使用方法，**提高工作效率**，就总结了一些常用快捷键使用方法。满足一般需求，掌握基本增、删、改、查就可以了，近一步学习可以了解多屏操作和宏的使用以及自定义插件功能。

Linux发行版服务器基本上是已经配置好 vi 或者 vim，可以使用进行练习，也可以下载vim客户端（支持多个平台：Linux、macOS、Windows）软件进行练习，当然还使用git bash一样可以进行练习。目前主流IDE工具，基本上是支持安装vim插件，开启插件支持vim相关功能。例如：VSCode、IntelliJ IDEA（社区版与旗舰版均支持）。

<!-- more -->


展示一下Windows平台下的vim以及gvim：

vim：在字符界面进行使用，可以看到初次进入会显示版本信息、维护人以及一些帮助命令。

[![pp9CGA1.png](https://s1.ax1x.com/2023/02/26/pp9CGA1.png)](https://imgse.com/i/pp9CGA1)



GVIM：其实是GUI VIM，带有图形操作界面，便于桌面客户端使用。

[![pp9CKcF.png](https://s1.ax1x.com/2023/02/26/pp9CKcF.png)](https://imgse.com/i/pp9CKcF)



**VSCode使用vim插件，简单介绍一下**

ctrl + shift + p：快速掉出命令行工具，键入vim找到Toggle Vim Mode

[![pp9kna9.png](https://s1.ax1x.com/2023/02/26/pp9kna9.png)](https://imgse.com/i/pp9kna9)



# shell或者其它terminal快速纠错

掌握常用快捷键提高日常工作效率，某些快捷键并不适用Windows terminal。

- ctrl + h ：删除上一个字符，ctrl + w：删除上一个单词，ctrl + u： 删除一整行；
- ctrl + a：跳到行首，在Windows terminal是全选；ctrl + e：跳到行末，不适用Windows terminal；
- ctrl + b：前移，不适用Windows terminal；ctrl + f：后移，不适用Windows terminal。

**tips**：Windows terminal快速跳转，使用ctrl + 左右方向键进行跳转。



# vim入门实战

vim官网：[https://www.vim.org/](https://www.vim.org/)

开源仓库：[https://github.com/vim/vim](https://github.com/vim/vim)

插件查找：[https://vimawesome.com/](https://vimawesome.com/)

使用VimAwesome检索自己需要的插件，基本上每个插件列出了源地址。通常个人习惯从github上克隆，比较方便。

[![pp9CacD.png](https://s1.ax1x.com/2023/02/26/pp9CacD.png)](https://imgse.com/i/pp9CacD)



唯有多练才能熟练，善用自带帮助文档，如下列举最基本帮助文档以及分屏操作获取方式。
**注意**：使用格式为英文输入法下的冒号加上help，使用命令亦是如此。

```bash
:help
:help vs
:help sp
```

**插入（编辑）模式**：a 	i 	o。插入模式姿势也很多啊，标准姿势 i ，高难度姿势 a、o。

- a：节奏插，在当前字符光标前一个字符插入

- i：慢插，当前光标位置插入。

- o：快插，快速在前一行下方插入一行空白行



**快速终止**（进入插入模式），等价于ESC退出编辑模式进入normal模式

- ctrl + [

- ctrl + c


养成使用 hjkl 按键替代方向键进行上下左右移动，提高操作效率。



# vim快速移动

**normal模式**

**快速移动**：按住快捷键 h j k l

- h：左移
- j：下移
- k：上移
- l：右移



**单词切换**

- w\W
- b\B
- e



**搜索移动**（行间）

- f\F：按住f输入单词，使用逗号（,），分号（;）切换单词。
- t：转到输入字符前一个字符上。



**水平移动**

- 0：移动到行首第一个字符
- ^：移动到第一个非空白字符
- $：移动到行尾，g_ 移动到非空白行尾



**页面快速移动**

- ctrl + u： 上翻页，等同于shift + 方向键上键
- ctrl + f： 下翻页，等同于shift + 方向键下键
- gg :快速回到页面顶部。

更多用法，可以参考
```bash
:help g
```



# vim增删改查

vi：选择多个字符，等同于shift + v：选择当前行，使用G选择余下行。 

**normal模式下使用**

删除

- x：快速删除一个字符
- d（delete）：配合文本对象快速删除一个单词：dw；快速删除一行：dd
- d和x：配合数字执行多次

新增

- 插入数据（a	i	o）

修改

- r\R（replace）：以...替代，替代当前字符，R：替代后续字符
- c（change）：改变，cc：删除当前行，cw（ciw、caw）：删除当前单词并修改
- s\S（substitute）：替代，删除当前字符并进行插入，可以在normal模式替代插入模式；S：删除整行

恢复

- u：恢复到之前的状态，删掉插入内容。



**搜索替换**

- s\S（substitute），可以配合正则表达式替换
- 替换位标志：g（global），c（confirm），n（number）
- :% s/word/w/g：全局替换
- :% s/\\<word\\>/w/g：精确匹配单词后替换



# vim多屏操作

[![pp9CDHA.png](https://s1.ax1x.com/2023/02/26/pp9CDHA.png)](https://imgse.com/i/pp9CDHA)



**normal模式**

**多文件操作，准备多个文件用于测试**

预先准备多个测试文件，使用vim或者touch命令都行

vim test_a.txt

```bash
this is test_a file
# test a
```

复制多个文件用于测试：

```bash
cp test_a.txt test_b.txt;cp test_a.txt test_c.txt
```

开始测试，依次输入如下命令：

- :e test_a.txt，:e test_b.txt，:e test_c.txt
- :ls
- :bprevious

使用 :e 进入编辑模式，不退出当前会话同时编辑多个文件，:ls 查看当前会话缓存文件，:bprevious 查看之前编辑过的文件。

[![pp9CJtx.png](https://s1.ax1x.com/2023/02/26/pp9CJtx.png)](https://imgse.com/i/pp9CJtx)



**多屏操作**

- :vs：水平分割
- :sp：垂直分割
- ctrl + w ：移动窗口，配合大写L和hjkl操作



水平分割效果展示

[![pp9C0nH.jpg](https://s1.ax1x.com/2023/02/26/pp9C0nH.jpg)](https://imgse.com/i/pp9C0nH)



垂直分割效果展示

[![pp9CN9K.jpg](https://s1.ax1x.com/2023/02/26/pp9CN9K.jpg)](https://imgse.com/i/pp9CN9K)



更多用法，参考帮助文档
```bash
:help vs
:help sp
```



**多个标签页**

- :tabnew ：打开新的标签页
- :tabnext：切换标签页
还可以使用快捷键 gt 快速切换标签页，同样可以使用简化写法 :tabn 切换标签页。
[![pp9CU1O.jpg](https://s1.ax1x.com/2023/02/26/pp9CU1O.jpg)](https://imgse.com/i/pp9CU1O)

更多用法，参考帮助文档
```bash
:help tabnew
:help tabnext
```

**复制粘贴**

- normal下使用y（yank）复制，p（put）粘贴
- yy：复制一行
- yiw：复制一个单词
- x删除，p粘贴。

示例：如果复制一大段内容，可以结合快捷键shift + v 配合 y复制，使用 p 粘贴内容。
[![pp9Cdje.jpg](https://s1.ax1x.com/2023/02/26/pp9Cdje.jpg)](https://imgse.com/i/pp9Cdje)

打开了多个分屏或者标签页，如何一次性关闭？使用 :qa 命令关闭全部，返回当前终端。




# vim进阶

**normal模式**

**vim宏**

- 按住 q 键录制类容，配合使用命令qa
- 快速选择余下所有行：shift + v  G
- 进入普通模式输入：:normal @a



**常用补全**

- ctrl + n 和 ctrl + p 补全单词
- ctrl + x 和 ctrl + f 补全文件名
- ctrl + x 和 ctrl + o 补全代码

补全如果没生效，需要配置相应的插件。



**使用vim相关插件，修改配色方案**

以Java类为示例进行说明，编辑Java代码Hello world

`vim Hello.java`

```bash
class Hello{
        public static void main(String args[]){
                System.out.println("Hello cangls");
        }
}
```



克隆hybrid配色方案

```bash
git clone https://github.com/w0ng/vim-hybrid.git
```

创建文键目录

```bash
mkdir -p .vim/colors
```

复制hybrid.vim到.vim/colors目录中

```bash
cp vim-hybrid/colors/hybrid.vim  .vim/colors
```

编辑配色方案

```bash
vim Hello.java
:colorscheme hybrid
```

[![pp9ktVH.png](https://s1.ax1x.com/2023/02/26/pp9ktVH.png)](https://imgse.com/i/pp9ktVH)

修改配色方案永久生效，设置`background=dark`为暗色系，默认为light浅色系，默认设置显示行号`set number`

vim .vimrc
```bash
set background=dark
colorscheme hybrid
set number
```



恢复默认配色

```bash
:colorscheme default
```

## vim插件
初次使用，插件不在多，在于对你的操作有所提升。可以一步步尝试安装插件，对比哪些对你的日常工作有帮助。


- vim-plug：用于管理插件。
- NERDTree：用于增强目录树插件。
- TarBag：用于显示标签插件（需要ctags支撑，Windows平台将ctags.exe文件置于vim根目录同级即可使用）
例如：个人解压后vim路径：D:\gvim_9.0.1075_x64\vim90\，将ctags.exe放入vim90目录即可。

如果当前用户根目录没有.vimrc 文件，则新增。

Windows平台需要在当前用户新增 .vimrc 文件。
```powershell
vim ~\.vimrc
```
Linux平台一样需要新增 .vimrc
```bash
vim ~/.vimrc
```

Rocky 9 Linux 平台如下操作
```bash
wget https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim 
--directory-prefix=/usr/local/share/vim/vim90/autoload/
```
下载文件，如何指定保存路径？通过帮助文档查询：
```bash
[root@localhost ~]# wget --help | grep "保存文件"
  -P,  --directory-prefix=前缀     保存文件到 <前缀>/..
```

如果没有 wget 工具，请先安装：
```bash
dnf -y install wget
```


Windows 平台，访问直接下载：
[https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim)


复制到你安装 vim 后，生成 autoload 所在目录，比如：D:/vim90/autoload/


安装 vim-plug 插件后，加入如下内容即可安装 nerdtree 和 tagbar 插件：
```bash
set number
call plug#begin()
  Plug 'preservim/nerdtree'
  Plug 'preservim/tagbar'
call plug#end()
```
个人认为，这两个插件还是很实用的，尤其是浏览代码。

Rocky 9 Linux 平台，如果想 tagbar 正常运行，同样需安装 ctags 软件包：
```bash
dnf -y install ctags
```

插件安装命令： 
```bash
:PlugInstall
```
插件安装后，重启vim即可生效。

安装插件效果展示，最左侧是nerdtree效果，最右侧是tagbar效果。

示例：
```bash
vim Test.java
:NERDTree
:Tagbar
```

[![pp9CYh6.jpg](https://s1.ax1x.com/2023/02/26/pp9CYh6.jpg)](https://imgse.com/i/pp9CYh6)




## vim无处不在

**vim与Tmux**可以在Linux服务器上安装tmux配合vim使用，效果更加。

Linux发行版（centos9-stream）安装tmux

```
[root@Centos9-Stream ~]# yum list | grep tmuxtmux.x86_64                                          3.2a-4.el9                         baseos[root@Centos9-Stream ~]# yum -y install tmux[root@Centos9-Stream ~]# rpm -qa | grep tmuxtmux-3.2a-4.el9.x86_64
```

安装后初步使用：

```
[root@Centos9-Stream ~]# tmux ls0: 1 windows (created Sun Feb 26 15:42:19 2023) (attached)
```

默认进入tmux，使用tab键可以提示相关命令，使用exit退出tmux。

[![pp9C1B9.png](https://s1.ax1x.com/2023/02/26/pp9C1B9.png)](https://imgse.com/i/pp9C1B9)





**IDE与vim**

- VSCode(Visual Studio Code)
- STS4(Spring Tool Suite4)
- IDEA(IntelliJ IDEA) 

**文初演示了VSCode使用vim插件，此处展示一下STS4使用vim插件：**

01、STS4启动界面

[![pp9ClnJ.png](https://s1.ax1x.com/2023/02/26/pp9ClnJ.png)](https://imgse.com/i/pp9ClnJ)



02、顶部菜单栏找到help，打开**Eclipse Marketplace**

[![pp9Cu1U.png](https://s1.ax1x.com/2023/02/26/pp9Cu1U.png)](https://imgse.com/i/pp9Cu1U)





**03、搜索vim并安装**

[![pp9CMX4.png](https://s1.ax1x.com/2023/02/26/pp9CMX4.png)](https://imgse.com/i/pp9CMX4)



**04、重启开发工具STS4，初始化界面效果**

[![pp9C37R.png](https://s1.ax1x.com/2023/02/26/pp9C37R.png)](https://imgse.com/i/pp9C37R)



**vim与neovim**
与时俱进，竞争产出新特性。
https://github.com/neovim/neovim




**站在巨人的肩膀上，打造炫酷的vim**
SpaceVim：https://github.com/SpaceVim/SpaceVim


个人收藏一些vim相关插件仓库地址：https://github.com/stars/cnwangk/lists/vim

你还可以通过 vimawesome 寻找vim插件：https://vimawesome.com


以上总结，仅供参考哟，希望对你的工作有所帮助！

—END—