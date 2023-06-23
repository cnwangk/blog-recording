---
title: hugo初体验
date: 2023-04-14 21:13:53
tags: hugo
categories:
- 静态博客
---

centos-stream-9 初体验hugo，初体验比较简化，只拿了一篇示例文章进行体验。



### centos-stream-9 环境

**准备环境**：

- hugo
- git

**说明**：git 环境不是必要环境，如果你从远程仓库获取资源（比如获取 hugo 相关的主题），是需要 git 环境的。同时便于版本控制以及上传至提供 pages 服务的平台，比如 github 和 gitee。



### git & hugo 部署

git 在线安装方式yum & dnf工具：

```bash
yum -y install git
dnf -y install git
```

如何配置 git 环境，可在站内搜索 git 相关教程，这里不再赘述。



hugo快速开始文档：

```bash
hugo new site quickstart
cd quickstart
git init
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
echo "theme = 'ananke'" >> config.toml
hugo server
```



**如下，是在Linux发行版 centos-stream-9 平台hugo的简易使用方法**。

获取hugo：
```bash
wget https://github.com/gohugoio/hugo/releases/download/v0.111.3/hugo_0.111.3_linux-amd64.tar.gz
```



解压：

```bash
tar -zxvf hugo_0.111.3_linux-amd64.tar.gz
```



新建blog站点：

```bash
./hugo new site blog
```


切换工作空间：

```bash
cd blog/
```


blog目录文件列表：

```bash
archetypes  assets  config.toml  content  data  layouts  public  resources  static  themes
```



git 初始化：

```bash
git init
```



获取 hugo ananke主题：

```bash
git submodule add https://github.com/theNewDynamic/gohugo-theme-ananke themes/ananke
```



运行服务：

```bash
./hugo server
```

停止服务，使用快捷键：

```bash
ctrl + c
```



测试，打开终端：看到终端有 html 代码展示，证明运行成功。 

```bash
curl http://127.0.0.1:1313
```

此时还不具备远端访问，需要绑定远程 IP 地址。如果安装了防火墙管理工具，比如firewalld服务，需要手动放通端口1313：

```bash
firewall-cmd --zone=public --add-port=1313/tcp --permanent
firewall-cmd --reload
```



指定ip地址运行：

```bash
/opt/workspace/blog-hugo-prod/hugo server --bind 192.168.245.132
```
**说明**：/opt/workspace/blog-hugo-prod/ 目录是解压后hugo脚本所在目录。



查看当前使用 hugo 版本：

```bash
[root@Centos9-Stream blog]# /opt/workspace/blog-hugo-prod/hugo version
hugo v0.111.3-5d4eb5154e1fed125ca8e9b5a0315c4180dab192 linux/amd64 BuildDate=2023-03-12T11:40:50Z VendorInfo=gohugoio
```



复制已经制作完成的博客试验品到 /content/posts/ 目录下：

```bash
cp vim入门实战.md  /opt/workspace/blog-hugo-prod/blog/content/posts/
```

**注意**：规范格式，参考 hugo 文档给出的示例

```bash
---
title: "My First Post"
date: 2022-11-20T09:03:20-08:00
draft: true
---
## Introduction

This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!
```

hugo 配置文件 config.toml：

```bash
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'ananke'
```



再次运行：

```bash
/opt/workspace/blog-hugo-prod/hugo server --bind 192.168.245.132
```



访问示例：

[http://192.168.245.132:1313/](http://192.168.245.132:1313/)


### 使用 hugo-theme-next 主题

可能会遇到如下问题：
```bash
[root@localhost blog]# ./hugo server --bind 192.168.245.133
Start building sites …
hugo v0.111.3-5d4eb5154e1fed125ca8e9b5a0315c4180dab192 linux/amd64 BuildDate=2023-03-12T11:40:50Z VendorInfo=gohugoio
WARN 2023/05/15 22:39:52 Hugo NexT 主题使用了 SCSS 框架，请到官方地址下载 Hugo Extended 版本：https://github.com/gohugoio/hugo/releases
ERROR 2023/05/15 22:39:52 Because that use SCSS framework in Hugo NexT, Please download Hugo extended version on offical site: https://github.com/gohugoio/hugo/releases
Error: Error building site: TOCSS: failed to transform "main.scss" (text/x-scss). Check your Hugo installation; you need the extended version to build SCSS/SASS with transpiler set to 'libsass'.: this feature is not available in your current Hugo version, see https://goo.gl/YMrWcn for more information
Built in 47 ms
```

文初介绍使用 hugo 版本是非扩展版本（Extended），提示我们下载：请到官方地址下载 Hugo Extended 版本：
[https://github.com/gohugoio/hugo/releases](https://github.com/gohugoio/hugo/releases) 


获取 Hugo Extended 版本：
```bash
wget https://github.com/gohugoio/hugo/releases/download/v0.111.3/hugo_extended_0.111.3_linux-amd64.tar.gz
```

解压 hugo_0.111.3_linux-amd64.tar.gz 到指定目录：
```bash
mkdir /opt/workspace/blog-hugo-prod/  # 新建 hugo blog 工作空间
tar -zxvf hugo_0.111.3_linux-amd64.tar.gz  --directory=/opt/workspace/blog-hugo-prod/ # -C, --directory=DIR 指定解压目录
```

再次执行，正常运行：
```bash
./hugo server --bind 192.168.245.133
```


### hugo 在线初体验

个人搭建简单示例，已上传至cloudflare，可访问体验：

[https://blog-wangk-hugo.pages.dev/](https://blog-wangk-hugo.pages.dev/)



感兴趣的可以前往    [https://dash.cloudflare.com/](https://dash.cloudflare.com/)    注册账号，然后选择 Pages，创建项目部署你的个人站点。



**个人搭建的实验品**：

- hexo：[https://cnwangk-github-io.pages.dev/](https://cnwangk-github-io.pages.dev/)

- jekyll：[https://blog-wangk.pages.dev/](https://blog-wangk.pages.dev/)

- hugo：[https://blog-wangk-hugo.pages.dev/](https://blog-wangk-hugo.pages.dev/)

  



**参考资料**：

- hugo文档：[https://gohugo.io/getting-started/quick-start/](https://gohugo.io/getting-started/quick-start/)
- hugo仓库：[https://github.com/gohugoio/hugo](https://github.com/gohugoio/hugo)



—END—