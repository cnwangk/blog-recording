---
title: Windows 平台使用 hexo 搭建个人博客
date: 2022-03-15 
tags: hexo
categories: 
- 静态博客
---



Windows 平台使用 hexo 搭建个人博客。

既学了 git 和 github 的用法，也熟悉了 nodejs。

又多了一项打发业余时间的软技能。慢慢地变成硬技能，何乐而不为？


如果你从旧版本 Next 主题升级上来，请戳这篇 issues，相信会对你有所帮助：

[https://github.com/next-theme/hexo-theme-next/issues/4](https://github.com/next-theme/hexo-theme-next/issues/4)

<!-- more -->


# Windows 平台使用 hexo 搭建私人博客

**必备环境（Windows）**：

- Nodejs：[https://nodejs.org/en/](https://nodejs.org/en/)（hexo 官方建议：Node.js 版本需不低于 10.13，建议使用 Node.js 12.0 及以上版本。）

- **提醒**：Node.js 14.0版本在运行hexo服务时会出现警告，**但不影响使用**，也可以升级更高版本。

  ```bash
  INFO  Start processing    # 使用nodejs 14.0出现警告，搜索后发现基本是让降版本至nodejs 12.0
  INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
  (node:4464) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
  (Use `node --trace-warnings ...` to show where the warning was created)
  (node:4464) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
  (node:4464) Warning: Accessing non-existent property 'filename' of module exports inside circular dependency
  (node:4464) Warning: Accessing non-existent property 'lineno' of module exports inside circular dependency
  (node:4464) Warning: Accessing non-existent property 'column' of module exports inside circular dependency
  (node:4464) Warning: Accessing non-existent property 'filename' of module exports inside circular dependency
  ```

- Git：[https://git-scm.com/downloads](https://git-scm.com/downloads)（个人使用版本：git version 2.31.1.windows.1）

- Hexo：[https://hexo.io/zh-cn/docs/github-pages](https://hexo.io/zh-cn/docs/github-pages)（个人使用版本：6.3.0）



**友情提醒**：如果只是想简单发点私人博客，landscape 主题完全可以满足。

**如果想看简洁的界面，又想有许多新功能，那就使用 Next 主题，这款主题持续更新**。



## 一  安装hexo

### 01  使用npm安装hexo环境

```bash
npm install -g hexo-cli   #使用npm安装Hexo-cli
npm install hexo          #使用npm安装Hexo，熟悉的用户可以仅局部安装Hexo包
```

做完上面操作，恭喜你可以进行初始化安装blog文件了。



### 02  初始化博客（blog）目录


1、进入d盘（Windows terminal 下打开 cmd 或者 powershell）

```bash
cd d:
```

2、 创建hexo目录，方便自管理，知道这是使用hexo搭建的博客

```bash
mkdir hexo
```

3、 切换到hexo目录

```bash
cd hexo
```

4、 初始化blog目录，如果速度很慢，建议替换为国内镜像源地址

```bash
hexo init blog
```

5、 新增md文件

```bash
hexo new "hello my blog"
```
生成md（markdown）文件所在目录：source      

6、 生成静态文件

```bash
  hexo g
```
生成静态文件所在目录：public

7、 启动服务

```bash
hexo s
```
或者指定 ip 地址和 port（端口）
```bash
hexo clean && hexo s -i 192.168.0.233 -p 4001
```





## 二  切换 nodejs 镜像源

nodejs 临时配置国内 taobao 镜像源。

npm 镜像源地址，国内镜像站：
>  [https://npmmirror.com/](https://npmmirror.com/)

nodejs 临时配置国内 taobao 镜像源：
> npm config set registry http://registry.npm.taobao.org/





## 三  安装插件（进阶）

如果你会一丢丢前端（nodejs）知识，对这些插件使用会很顺手。

1、 安装hexo插件（Next主题）
```bash
npm install hexo-xxx-xxx --save
```

安装插件目录：node_modules

**比较实用的几个插件**：部分对landscape适用，主要是对Next主题适用。

- hexo-auto-excerpt：配置阅读全文功能，主页实现折叠效果（或者使用手动截断：<!-- more -->）。
- hexo-generator-sitemap：Next主题配置站点。
- hexo-leancloud-counter-security：配置博客阅读次数，需要在leancloud注册并配置应用凭证、结构化数据。
- hexo-generator-searchdb：Next主题配置本地搜索，注意在hexo中也需要配置。


**这里只详细介绍主题配置自动阅读**（landscape和Next都适用）：

```yaml
# 1. 在主题（Next或者landscape）中设置_yaml.config配置文件，添加如下配置文件
#https://github.com/ashisherc/hexo-auto-excerpt
auto_excerpt: 
  enable: true
  length: 100
```

**cmd命令执行以下命令**：
```bash
# 2. 测试效果（Windows下使用cmd命令）
hexo g    # 生成静态文件
hexo s    # 启动服务
```

**测试访问**：
> http://localhost:4000



2、 主题目录

**主题所在目录**：themes

**获取Next主题**：使用 git clone 或者直接下载

> git clone git@github.com:next-theme/hexo-theme-next.git
>
> [https://github.com/next-theme/hexo-theme-next/archive/refs/heads/master.zip](https://github.com/next-theme/hexo-theme-next/archive/refs/heads/master.zip)


下载后复制到themes目录，然后**修改hexo配置文件**_config.yml：
```yaml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: hexo-theme-next
#theme: landscape
```

如果使用 npm 命令安装 next 主题：
```bash
npm install hexo-theme-next --save
```

在 hexo 配置，需要变动：
```yaml
theme: next
```
还需要复制一份配置到 blog 根目录：
```bash
cp .\node_modules\hexo-theme-next\_config.yml ._config.next.yml
```


3、 hexo配置文件

 blog目录下配置文件： _config.yml

**介绍一些使用比较多的参数**：更多请参考 hexo 或者 Next 主题文档
```yaml
# Site    #站点配置
title:    #网站标题：养得胸中一种恬静
subtitle:   #子标题
description:  #描述（个人简介）：莫问收获，但问耕耘
author:     #作者
language: zh-CN #配置语言（中文）

# search  #搜索
search:
  path: search.xml
  field: post
  content: true
  format: html
  
# Deployment  #配置一键发布，需要获取github的私人令牌（token）
## Docs: https://hexo.io/docs/one-command-deployment
#deploy:
#  type: git
#  repo: https://github.com/username/username.github.io
#  example, https://github.com/hexojs/hexojs.github.io
#  branch: gh-pages
```


4、 主题配置文件

themes目录landscape主题（hexo默认主题）： _config.yml

themes目录next主题hexo-theme-next： _config.yml

**Next主题仓库**：

> [https://github.com/next-theme/hexo-theme-next](https://github.com/next-theme/hexo-theme-next)

**主要介绍一些个人配置Next主题重要部分**：根据使用经验加了注释

```yaml
menu:   #菜单配置
  home: / || fa fa-home               #主页
  about: /about/ || fa fa-user        #关于页面（个人简介），默认需要手动创建
  #search: /search                    #配置搜索
  tags: /tags/ || fa fa-tags          #配置标签页目录，默认需要手动创建
  categories: /categories/ || fa fa-th    #配置类别目录，默认需要手动创建
  archives: /archives/ || fa fa-archive   #配置归档目录
  schedule: /schedule/ || fa fa-calendar  #日程表
  sitemap: /sitemap.xml || fa fa-sitemap  #站点地图（xml文件，相当于一个导航）
  commonweal: /404/ || fa fa-heartbeat    #公益404界面，在source目录配置404.html即可

# Local Search  #配置本地搜索
# 下载插件：npm install hexo-generator-searchdb --save
# Dependencies: https://github.com/next-theme/hexo-generator-searchdb 
local_search:
  enable: true
  # If auto, trigger search by changing input.
  # If manual, trigger search by pressing enter key or search button.
  trigger: auto
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # Unescape html strings to the readable one.
  unescape: false
  # Preload the search data when the page loads.
  preload: false


#安装sitemap插件
#npm install hexo-generator-sitemap --save
#npm install hexo-generator-baidu-sitemap --save
# 自动生成sitemap
sitemap:
  path: sitemap.xml
  
#导航栏在左侧、中间或者右侧
sidebar:
  # Sidebar Position.
  position: left  

#配置社交信息
social:
  GitHub: https://github.com/cnwangk || fab fa-github
  E-Mail: mailto:dywangk@gmail.com || fa fa-envelope

#配置阅读全文效果
#https://github.com/ashisherc/hexo-auto-excerpt
auto_excerpt: 
  enable: true
  length: 100  

#你主打的写作平台（比如公众号）
follow_me:
  WeChat: /images/wechat_channel.jpg || fab fa-weixin #设置公众号二维码，后台下载自己的二维码

#配置代码高亮显示（默认是github浅色）
codeblock:
  # Code Highlight theme
  # Available value: 
  # https://github.com/chriskempson/tomorrow-theme
  #highlight_theme: night eighties
  # All available themes: https://theme-next.js.org/highlight/
  theme:
    #light: default
    light: atom-one-dark
    dark: stackoverflow-dark  
    
# Baidu Analytics  #百度站点分析
# See: https://tongji.baidu.com
baidu_analytics: #注册账号建立分析站点生成的ID（一串字符串）
```


更多配置说明，请参考Next主题文档介绍：

> [https://theme-next.js.org/](https://theme-next.js.org/)



## 四  发布至github pages

1、 发布至github pages

**前提**：已经配置 git 环境（本地生成ssh公钥，然后配置到github）

如果你还没自己的 github 账号，也没配置 git 环境，可以参考我的历史博客：**git推送项目到github并使用gitee做镜像仓库**，如果图片被防盗链了，还可以在我的公众号上搜索查看。
    
也可以配置 deploy 一键发布，需要配置 github 私人令牌 token。
    
个人推荐使用 cp 命令将 public 目录下生成的静态文件复制到你的 repo（仓库），然后提交到远程仓库，这样操作更灵活一点。


**如下为提交至远程仓库详细步骤**：

```bash
mkdir github # 1. 创建github目录，用于存放（检出）自己的远程仓库
git clone git@github.com:yourUserName/yourUserName.github.io.git # 2. 克隆远程仓库
cd yourUserName.github.io   # 3. 切换到仓库
git branch gh-pages       # 4. 创建分支gh-pages
git remote add origin git@github.com:yourUserName/userName.github.io.git # 5. 连接远程仓库，已连接会提示exists
git add --all         # 6. 暂存所有有文件
git commit -am "初始化提交"    # 7. 初始化提交所有文件  
git push git@github.com:yourUserName/yourUserName.github.io.git # 8. 推送至远程仓库
```

做完上面提交操作，还需要给github仓库配置github pages服务。

**github pages的配置页面**：

> [https://github.com/cnwangk/test/settings/pages](https://github.com/cnwangk/test/settings/pages)

**我测试配置了一个仓库**：2022最新版github pages配置界面

**注意**：仓库必须是公开的（public）、然后仓库命令可以命令为用户名加github.io。

默认进入一个设置好的**gh-pages**分支的仓库这样显示内容的：将gh-pages设置为默认仓库。

**Custom domain**：配置域名，比如userName.github.io之外的域名。

![](https://img-blog.csdnimg.cn/img_convert/5869739fcaf91e45e689fafd53ee9b65.png)


2、访问验证博客

```bash
https://yourUserName.github.io
```

可以访问我搭建好的示例：

> [https://cnwangk.github.io/](https://cnwangk.github.io/)



## 五  hexo帮助命令

1、 进入blog目录（cmd命令窗口）

```bash
cd blog
```

2、 执行帮助命令

 对使用比较有帮助的命令，根据个人实际使用经验，做了中文注释。

```bash
D:\hexo\blog>hexo --h             #查看帮助命令，使用Next主题
INFO  Validating config
INFO  ==================================
  ███╗   ██╗███████╗██╗  ██╗████████╗
  ████╗  ██║██╔════╝╚██╗██╔╝╚══██╔══╝
  ██╔██╗ ██║█████╗   ╚███╔╝    ██║
  ██║╚██╗██║██╔══╝   ██╔██╗    ██║
  ██║ ╚████║███████╗██╔╝ ██╗   ██║
  ╚═╝  ╚═══╝╚══════╝╚═╝  ╚═╝   ╚═╝
========================================
NexT version 8.10.1               #使用Next主题版本
Documentation: https://theme-next.js.org
========================================
Usage: hexo <command>

Commands:  # 命令
  clean       Remove generated files and cache. # 移除文件和缓存
  config      Get or set configurations.    # 获取和设置配置
  deploy      Deploy your website.        # 发布到你的网站
  generate    Generate static files.      # 生成静态文件
  help        Get help on a command.      # 获取帮助命令
  init        Create a new Hexo folder.     # 初始化，创建一个新的hexo目录
  lc-counter  hexo-leancloud-counter-security # 配置阅读数需要下载插件
  list        List the information of the site  #站点列表信息
  migrate     Migrate your site from other system to Hexo.  
  new         Create a new post.        #新建一个md（markdown）文件
  publish     Moves a draft post from _drafts to _posts folder.
  render      Render files with renderer plugins.
  server      Start the server.         #启动hexo服务
  version     Display version information.    #查看hexo版本

Global Options:
  --config  Specify config file instead of using _config.yml  #配置全局_config.yml文件
  --cwd     Specify the CWD
  --debug   Display all verbose messages in the terminal    #开启debug模式
  --draft   Display draft posts                 
  --safe    Disable all plugins and scripts           #禁用所有插件
  --silent  Hide output on console

For more help, you can use 'hexo help [command]' for the detailed information
or you can check the docs: http://hexo.io/docs/         #hexo官方文档
https://hexo.io/zh-cn/docs/                   #hexo中文文档
```



## 六  个人配置示例效果

[https://blog.cnwangk.top/](https://blog.cnwangk.top/)



# 莫问收获，但问耕耘

> 养得胸中一种恬静

以上就是本文的全部内容，希望能对你的工作与学习有所帮助。感觉写的好，就拿出你的一键三连。在公众号上更新的可能要快一点，目前还在完善中。**能看到这里的，都是帅哥靓妹**。如果感觉总结的不到位，也希望能留下您宝贵的意见，我会在文章中进行调整优化。


**tips**：使用hexo搭建的静态博客也会定期更新维护。


以上总结，仅供参考哟！希望对你有所帮助。

—END—



