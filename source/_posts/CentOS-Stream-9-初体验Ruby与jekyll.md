---
title: CentOS-Stream-9 初体验Ruby与jekyll
date: 2023-04-09 23:44:18
tags: jekyll
categories:
- 静态博客	
---


使用 jekyll 搭建测试环境，先上效果，访问即可体验：
[https://blog-wangk.pages.dev/](https://blog-wangk.pages.dev/)

![](https://s1.ax1x.com/2023/04/09/ppbB5Ps.png)

### 絮絮叨叨

**絮絮叨叨**
起初，在想自己有一定的 Hexo 使用经验，上手 jekyll 应该很快。实际动手，才发现没有想的那么容易。主要是Ruby、jekyll环境问题，遇到陌生没有接触过的技术，没有耐心阅读官方文档。遇到错误，没有耐心排查。

既然聊到 Hexo，那就简单说一下。如果你尝试搭建 Hexo 环境，需要准备 nodejs、npm 以及 git 环境。其中 git 环境用于版本控制和提交到远程仓库，使用jekyll 或者 hugo一样用得上。

如果你不想使用静态博客生成器生成，又有自己的一套技术栈（web后端和前端）。可以打造一套前后端分离的应用，部署到云服务器上，购买域名解析、备案。下面是我的大学老同学（六年 Java后端技术大佬）应该是使用ssm（spring + springboot + mybatis）以及 vuejs 打造的个人站点实验品**随想笔记**：

https://www.wxlzb.top/#/

![](https://s1.ax1x.com/2023/04/09/ppbDHfA.png)


有点扯远了，继续回到打造静态博客站点 jekyll 上。





**准备环境**：

1. Centos-stream-9（RHEL9系列）环境
2. Ruby环境
3. Ruby设置国内镜像源
4. Jekyll环境

当然，不一定要和我的环境一致，你可以在 Windows 平台搭建Ruby环境安装jekyll。



**CentOS-Stream 是什么**？

> Continuously delivered distro that tracks just ahead of Red Hat Enterprise Linux (RHEL) development, positioned as a midstream between Fedora Linux and RHEL. For anyone interested in participating and collaborating in the RHEL ecosystem, CentOS Stream is your reliable platform for innovation.

大意是：CentOS-Stream Redhat企业版Linux（RHEL）开发版本，定位在Fedora Linux 和 RHEL之间的中间流量。对于那些想参与并合作在RHEL生态系统中的人，CentOS Stream是你可靠的创新平台。

tips：Fedora Linux 很长一段时间作为Red Hat Enterprise Linux的上游版本（开发版本），Redhat作为稳定版本发行，centos同步更新Redhat资源进行发行。 


**Ruby是什么**？
> Ruby 是……
一门开源的动态编程语言，注重简洁和效率。Ruby 的句法优雅，读起来自然，写起来舒适。

**Jekyll是什么**？
> Transform your plain text into static websites and blogs.

大意是：你可以使用 jekyll 打造静态网站或者博客站点。



### centos-stream-9 部署

个人推荐使用虚拟机软件VMware搭建centos-stream-9 Linux环境，如果在Windows环境下一样可以使用WSL或者WSL2进行搭建。

**准备环境**：

1. VMware虚拟机软件
2. centos-stream-9 镜像

VMware官网：[https://www.vmware.com/products/workstation-pro.html](https://www.vmware.com/products/workstation-pro.html)

**关于VMware版本说明**

- VMware版本：关于VMware workstation pro 与  VMware workstation player。
- VMware workstation pro：付费服务，有完善的商业支持。
- VMware workstation player：面向个人PC用户的免费版本。前身是VMware player，直到VMware12版本开始成为pro版本的免费版本，购买商业支持后可升级为pro版本。

**centos-stream官网**：[https://www.centos.org/centos-stream/](https://www.centos.org/centos-stream/)


安装步骤：
1. 部署VMware。
2. 新建虚拟机（如果你使用VMware16，没有centos-stream-9选项，选Centos8即可）。
3. CD/DVD选择使用ISO镜像文件。
4. 进入centos-stream-9安装，没有特殊需求，默认回车即可，有图形化引导安装界面。

VMware成功部署 centos-stream-9 示例界面：

![](https://s1.ax1x.com/2023/04/09/ppbBIGn.png)

 安装了哪些环境，可以在描述一栏备注出来，这是一个好习惯。



### Ruby部署

关于Ruby部署，参考可靠资料：
ruby官网：[https://www.ruby-lang.org/zh_cn/](https://www.ruby-lang.org/zh_cn/)
ruby国内地址：[https://rubyinstaller.cn/](https://rubyinstaller.cn/)
ruby开源仓库地址：[https://github.com/ruby/ruby](https://github.com/ruby/ruby)

主要有两种部署方式：
- 源码包 & 二进制包
- rbenv管理工具

**个人使用如下部署方式**
yum & dnf源部署：

```bash
dnf -y install ruby ruby-devel gcc g++ make cmake
```

版本查看：
```bash
ruby -v;gem -v;gcc -v;g++ -v;make -v 
```

rbenv部署：

```bash
yum -y install rbenv
```


rbenv版本查看：
```bash
rbenv -v
rbenv 1.2.0
```

rbenv仓库地址：[https://github.com/rbenv/rbenv](https://github.com/rbenv/rbenv)

**Ruby设置国内镜像源**

- Ruby阿里源：[https://developer.aliyun.com/mirror/rubygems](https://developer.aliyun.com/mirror/rubygems)
- Ruby清华大学源：[https://mirrors.tuna.tsinghua.edu.cn/help/rubygems](https://mirrors.tuna.tsinghua.edu.cn/help/rubygems)
- Ruby腾讯源：[https://mirrors.cloud.tencent.com/rubygems/](https://mirrors.cloud.tencent.com/rubygems/)
- Ruby华为云源：[https://repo.huaweicloud.com/repository/rubygems/ ](https://repo.huaweicloud.com/repository/rubygems/)
- Ruby中国科技大学源：[https://mirrors.ustc.edu.cn/rubygems/](https://mirrors.ustc.edu.cn/rubygems/)


示例：打开终端运行移除默认源，配置阿里源
```bash
gem sources 	#查找默认源
gem sources --remove https://rubygems.org/  			#移除默认源
gem sources -a https://mirrors.aliyun.com/rubygems/  	#配置阿里源
```

使用 Gemfile 和 Bundler，可以这样配置：
```bash
bundle config mirror.https://rubygems.org  https://developer.aliyun.com/mirror/rubygems
```

如果想配置其它ruby国内镜像镜像源，只需要更换 sources 后面追加的地址即可。

同理，如果想加速安装Ruby环境，同样可以在这些国内开源镜像网站寻找安装包进行安装。如何获取软件安装包：如果有wget命令环境，直接在wget后面追加软件镜像仓库地址即可。


示例下载 Ruby 和openjdk：
```bash
wget https://repo.huaweicloud.com/ruby/ruby/3.2/ruby-3.2.1.tar.gz
wget https://repo.huaweicloud.com/openjdk/17.0.2/openjdk-17.0.2_linux-x64_bin.tar.gz
```



### Jekyll部署

jekyll官网：https://jekyllrb.com/


gems部署，安装jekyll服务：
```bash
gem install jekyll bundler
```

jekyll获取帮助命令：
```bash
jekyll --h
```



**发布之前，准备必要环境**：

- git 本地环境
- github 仓库环境

**注意**：github 仓库需要手动开启 pages 服务，创建分支命名为 gh-pages。

如果你还没有 github 账号，如果你还没有创建 github pages 服务仓库，如果你还没有 git 环境。没关系，可以参考本人公众号里面github基础教程《git推送项目到github并使用gitee做镜像仓库》以及《你真的了解git、gitee、github吗》。虽然写的稀烂，但可以进行参考。



**发布到提供 pages 服务的网站**：

- github pages
- gitee pages
- cloudflare pages

文初演示地址，采用cloudflare pages服务，支持直接上传本地目录以及压缩包，需要注意中文编码问题。

个人不推荐直接上传，习惯使用如下步骤：

1. 发布：github 仓库
2. 关联：第三方 pages 服务
3. 同步至第三方 pages 服务：cloudflare、netlify、vercel。



### Jekyll：人生中的第一篇博客

1. jekyll new blog：新建博客（项目）空间
2. cd blog：进入博客（项目）空间
3. bundle exec jekyll serve ：启动 jekyll 服务，默认访问地址：localhost:4000

```bash
jekyll new blog
cd blog
bundle exec jekyll serve 
```
关于jekyll服务启动，你还可以使用如下简化方式：

```bash
jekyll s --h=192.168.245.132
```

**注意**：**如果在服务器环境不指定IP地址，无法访问远程地址**，使用curl命令测试访问localhost:4000或者127.0.0.1:4000则是正常显示。


打开浏览器，访问：http://192.168.245.132:4000，如果只在本地访问：http://127.0.0.1:4000

或者使用curl命令测试：
```bash
[root@Centos9-Stream soft]# curl -X GET http://192.168.245.132:4000 | grep "Welcome to Jekyll!"
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4788  100  4788    0     0  2337k      0 --:--:-- --:--:-- --:--:-- 2337k
            Welcome to Jekyll!
```

其实，仔细观察，会发现初始_posts目录下博文给了我们示范：日期-文章标题.后缀名
```bash
2023-04-07-welcome-to-jekyll.markdown
```
接下来看一看，官方文档给出的创建文章规范。

**创建文章规范**

发表一篇新文章，你需要在_post目录中创建一个新文件，文件名的命名非常重要。Jekyll 要求一篇文章的文件名遵循下面的格式：
- 格式一：年-月-日-标题.MARKUP
- 格式二：年-月-日-标题.md 
- 格式三：年-月-日-标题.markdow
- 格式四：年-月-日-标题.textile


日期格式遵循：年是 4 位数字，月和日都是 2 位数字。MARKUP扩展名代表了这篇文章是用什么格式写。下面是一些合法的文件名的示例：
```bash
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.textile
```

注意：新建文章需要按照示例博文规范，日期-标题.md。

示例：2023-02-26-vim入门实战.md，新建文章复制到指定目录_posts
```bash
cp 2023-02-26-vim入门实战.md _posts/
```
起初我以为将hexo生成静态博客 posts 目录复制到jekyll posts目录下即可。再次阅读官方文档，发现需要遵循一定的命名规范，还比较严格，整体体验感觉没有 Hexo 友好。



**排查错误**：

```bash
[root@Centos9-Stream blog]# jekyll b
Resolving dependencies...
Configuration file: /opt/workspace/blog-jekyll-prod/blog/_config.yml
            Source: /opt/workspace/blog-jekyll-prod/blog
       Destination: /opt/workspace/blog-jekyll-prod/blog/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
Deprecation Warning: Using / for division outside of calc() is deprecated and will be removed in Dart Sass 2.0.0.

Recommendation: math.div($spacing-unit, 2) or calc($spacing-unit / 2)

More info and automated migrator: https://sass-lang.com/d/slash-div
...
Warning: 6 repetitive deprecation warnings omitted.
Run in verbose mode to see all warnings.
                    done in 0.466 seconds.
 Auto-regeneration: disabled. Use --watch to enable.
```

参考github issues：[https://github.com/jekyll/minima/issues/709](https://github.com/jekyll/minima/issues/709)

编辑_config.yml文件：vim _config.yml
```yml
# _config.yml
sass:
  quiet_deps: true
```



### 借东风

查看个人已关联上的东风：如果想解除关联，同样在此页面进行配置。

[https://github.com/settings/installations](https://github.com/settings/installations)

![](https://s1.ax1x.com/2023/04/09/ppbBfaQ.png)



如下示例是个人使用 hexo 和 next主题打造的个人博客站点。当然，优化思考同样可以应用到jekyll或者hugo上。 关于 静态博客优化一点点思考。money & time 寻找平衡。

闲暇时间，想起自己很久没维护的hexo + nextjs打造的静态博客网站。访问速度龟速前进，比看小电影还慢。

一入编程深似海，从此节操是路人。这里是文某人网络三无（无廉耻、无节操、无页面）教程，希望对你有所帮助。



**思考**

静态博客网站老生常谈的两大问题：
1. 加载静态资源耗时长，使用cdn加速、压缩js、css、html文件，提高体验。
2. 访问国外网站速度慢，如果科学上网，速度还行。 其实你会发现，优化再优化最终归结到了科学上网，资源在国内访问速度自然没话说。

做完以上（压缩、CDN、套皮、科学上网）测试，可以在Chrome浏览器使用F12进行调试，找到Network，使用快捷键ctrl + r 查看css消耗时间对比，发现main.css加载耗时很长。

使用ctrl + f5大刷新：

- 套cf（cloudflare）皮：main.css加载时间300ms左右。
- 没套皮：main.css加载时间，运气不好，等待超过10s。
- 开加速光环：纵享丝滑，同样ms级别，也在300ms左右。
- nginx高性能服务器：访问加载速度一样很丝滑。

**tips**：浏览器有缓存机制，如果f5小刷新没生效，使用ctrl + f5大刷新或者 ctrl + shift + delete清除缓存进行尝试。



如果你访问是我原始没做啥优化也没套皮的这个地址：[https://wzgy.cnwangk.top](https://wzgy.cnwangk.top)   体验太糟糕了。

使用第三方平台同步github pages，如果同步过程访问github授权太慢，最好开个科学上网小工具（比如GreenHub）。



**需要做两件事**：

1. 在Vercel、cloudflare、netlify提供pages服务引入github pages仓库内容，设置自定义域名。
2. 在云服务器厂商购买域名，进行CNAME解析(域名映射)。



**以腾讯云域名控制台为示例进行DNS解析展示**：
[![pSxU5F0.jpg](https://s1.ax1x.com/2023/02/23/pSxU5F0.jpg)](https://imgse.com/i/pSxU5F0)



此处只展示基本配置、详细使用我相信各位道友比我还拿手。



**Vercel**

访问： [https://vercel.com](https://vercel.com)，同步github上的github pages 仓库即可。如果你使用CNAME值解析DNS，无需担心dns可能被污染的问题。

配置Domains（域名）：

[![pSxdUUI.jpg](https://s1.ax1x.com/2023/02/23/pSxdUUI.jpg)](https://imgse.com/i/pSxdUUI)



如果调试时，没有立即自动同步更新，可做如下尝试。通常来说，一段时间会自动同步过来。

[![pSxU7SU.jpg](https://s1.ax1x.com/2023/02/23/pSxU7SU.jpg)](https://imgse.com/i/pSxU7SU)



使用过程中，有可能遇到使用 git 提交github仓库，但是页面没有刷新过来。可能你遇到了和我一样的问题，**vercel 同步github pages仓库内容时，Deployments过程中进行 Running Checks失败了，需要手动skip all**。

![](https://s1.ax1x.com/2023/04/09/ppbBWVg.png)



个人搭建效果可供参考：[https://blog.cnwangk.top](https://blog.cnwangk.top)



**cloudflare**

官网：[https://www.cloudflarestatus.com](https://www.cloudflarestatus.com)
使用cloudflare pages服务，导入github pages服务仓库。与Vercel一样支持CNAME解析（域名映射）。
个人搭建效果可供参考：[https://cf.cnwangk.top](https://cf.cnwangk.top)



[![pSxUIYV.jpg](https://s1.ax1x.com/2023/02/23/pSxUIYV.jpg)](https://imgse.com/i/pSxUIYV)



**netlify**

访问：[https://app.netlify.com](https://app.netlify.com)，同步github上的github pages 仓库即可。同样支持CNAME解析（域名映射）。
个人搭建效果可供参考：[https://www.cnwangk.top](https://www.cnwangk.top)



[![pSxUoWT.jpg](https://s1.ax1x.com/2023/02/23/pSxUoWT.jpg)](https://imgse.com/i/pSxUoWT)

对比访问速度，下面套完皮后，感觉是不是还凑合。



**云服务器**

- 阿里云 & 腾讯云 & 华为云
- 学生优惠 & 首购优惠

使用云服务器，主要是高带宽比较贵，配置可以不用太高，安装字符界面足以满足日常需求。

安装nginx服务，将静态资源文件部署到html目录。

图片服务器也有着落了，使用MinIO & FastDFS搭建图片服务，目前个人比较推荐MinIO 。使用对象云存储对服务器压力要好很多，服务与图片分离开来，互不影响。

MinIO 中文官网下载地址：[https://www.minio.org.cn/download.shtml#/linux](https://www.minio.org.cn/download.shtml#/linux)

关于图片存储可以使用路过图床，如果想拥有更好的体验，**可以使用oos、cos、七牛云**这种付费对象云存储服务，什么都好，唯独需要money。

**注意**：在大陆使用域名需要备案，现在域名备案相对宽松，在腾讯云购买云服务器提供便捷备案。



**感受**

一朝笑尽天下事，从此节操是路人。没整理的时候，访问体验很糟糕，整完之后越来越糟糕，当然都是玩笑话。

cloudflare与Vercel、netlify使用体验相差无几，都支持CNAME解析（域名映射）。其实都差不多，如果非要挑一个出来，cloudflare体验稍微好一点点。

如果不想这么繁琐，可以使用国内平台gitee去构建gitee pages静态博客网站。

有经济条件，可以考虑购买云服务器（或者轻量级应用服务器）将静态博客文件使用高性能web服务器nginx进行托管。当然，nginx远不止这点功能，诸如反向代理、缓存、负载均衡等等比较强大的功能。

将生成的静态文件复制到 nginx 的 html 目录下即可，不用做任何改动。如果没有服务器，可以在 Windows 或者使用 VMware虚拟机搭建Linux环境安装nginx进行测试。关于nginx入门教程，可以在站内搜索：nginx入门到实践。

访问：[http://localhost](http://localhost)  或者 [http://127.0.0.1](http://127.0.0.1) ，体验还不错。



**参考资料**

- ruby官网：https://www.ruby-lang.org/zh_cn/
- jekyll doc：https://jekyllrb.com/docs/
- jekyll posts文档：https://jekyllrb.com/docs/posts/
- jekyll minima：https://github.com/jekyll/minima/issues/709


以上是我记录自己爬过的坑，希望对你有所帮助！

——END——