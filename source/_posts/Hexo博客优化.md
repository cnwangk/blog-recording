---
title: Hexo博客优化
date: 2023-03-11 22:41:35
tags: hexo 
categories: 
- 静态博客
---

关于 hexo 博客优化一点点思考。money & time 寻找平衡。

闲暇时间，想起自己很久没维护的hexo + nextjs打造的静态博客网站。访问速度龟速前进，比看小电影还慢。

一入编程深似海，从此节操是路人。这里是文某人网络三无教程，希望对你有所帮助。



## 思考

静态博客网站老生常谈的两大问题：
1. 加载静态资源耗时长，使用cdn加速、压缩js、css、html文件，提高体验。
2. 访问国外网站速度慢，如果科学上网，速度还行。 其实你会发现，优化再优化最终归结到了科学上网，资源在国内访问速度自然没话说。

做完以上测试（压缩、CDN、套皮、科学上网），可以在Chrome浏览器使用F12进行调试，找到Network，使用快捷键ctrl + r 查看css消耗时间对比，发现main.css加载耗时很长。
使用ctrl + f5大刷新：

- 套cf（cloudflare）皮：main.css加载时间300ms左右。
- 没套皮：main.css加载时间，运气不好，等待超过10s。
- 开加速光环：纵享丝滑，同样ms级别，也在300ms左右。
- nginx高性能服务器：访问加载速度一样很丝滑。



**tips**：浏览器有缓存机制，如果f5小刷新没生效，使用ctrl + f5大刷新或者 ctrl + shift + delete清除缓存进行尝试。



## 借东风

如果你访问是我原始没做啥优化也没套皮的这个地址：https://wzgy.cnwangk.top，体验太糟糕了。

使用第三方平台同步github pages，如果同步过程访问github授权太慢，最好开个科学上网小工具(比如GreenHub)。

**需要做两件事**：

1. 在Vercel、cloudflare、netlify提供pages服务引入github pages仓库内容，设置自定义域名。
2. 在云服务器厂商购买域名，进行CNAME解析(域名映射)。



**以腾讯云域名控制台为示例进行DNS解析展示**：
[![pSxU5F0.jpg](https://s1.ax1x.com/2023/02/23/pSxU5F0.jpg)](https://imgse.com/i/pSxU5F0)



此处只展示基本配置、详细使用我相信各位道友比我还拿手。

### Vercel
访问：[https://vercel.com ](https://vercel.com)

同步github上的github pages 仓库即可。如果你使用CNAME值解析DNS，无需担心dns可能被污染的问题。

配置Domains（域名）：

[![pSxdUUI.jpg](https://s1.ax1x.com/2023/02/23/pSxdUUI.jpg)](https://imgse.com/i/pSxdUUI)



如果调试时，没有立即自动同步更新，可做如下尝试。通常来说，一段时间会自动同步过来。

[![pSxU7SU.jpg](https://s1.ax1x.com/2023/02/23/pSxU7SU.jpg)](https://imgse.com/i/pSxU7SU)



个人搭建效果可供参考：[https://blog.cnwangk.top](https://blog.cnwangk.top)



### cloudflare

官网：[https://www.cloudflarestatus.com](https://www.cloudflarestatus.com)

控制台：[https://dash.cloudflare.com/](https://dash.cloudflare.com/)

使用cloudflare pages服务，导入github pages服务仓库。与Vercel一样支持CNAME解析（域名映射）。

个人搭建效果可供参考：[https://cf.cnwangk.top](https://cf.cnwangk.top)



[![pSxUIYV.jpg](https://s1.ax1x.com/2023/02/23/pSxUIYV.jpg)](https://imgse.com/i/pSxUIYV)



### netlify

访问：[https://app.netlify.com](https://app.netlify.com)

同步github上的github pages 仓库即可。同样支持CNAME解析（域名映射）。

个人搭建效果可供参考：[https://www.cnwangk.top](https://www.cnwangk.top)



[![pSxUoWT.jpg](https://s1.ax1x.com/2023/02/23/pSxUoWT.jpg)](https://imgse.com/i/pSxUoWT)

对比访问速度，下面套完皮后，感觉是不是还凑合。



## 云服务器

- 阿里云 & 腾讯云 & 华为云
- 学生优惠 & 首购优惠

使用云服务器，主要是高带宽比较贵，配置可以不用太高，Linux服务器安装字符界面足以满足日常需求。

部署nginx服务，将静态资源文件部署到html目录。

图片服务器也有着落了，使用**MinIO** & FastDFS搭建图片服务，目前个人比较推荐MinIO 。使用对象云存储对服务器压力要好很多，服务与图片分离开来，互不影响。

MinIO 中文官网下载地址：[https://www.minio.org.cn/download.shtml#/linux](https://www.minio.org.cn/download.shtml#/linux)

关于图片存储可以使用路过图床，如果想拥有更好的体验，**可以使用oos、cos、七牛云**这种付费对象云存储服务，什么都好，唯独需要money。**注意了**：在大陆使用域名需要备案，现在域名备案相对宽松，在腾讯云购买云服务器提供便捷备案。







## 感受

一朝笑尽天下事，从此节操是路人。没整理的时候，访问体验很糟糕，整完之后越来越糟糕，当然都是玩笑话。

cloudflare与Vercel、netlify使用体验相差无几，都支持CNAME解析（域名映射）。其实都差不多，如果非要挑一个出来，cloudflare体验稍微好一点点。

如果不想这么繁琐，可以使用国内平台gitee去构建gitee pages静态博客网站。

有经济条件，可以考虑购买云服务器（或者轻量级应用服务器）将静态博客文件使用高性能web服务器nginx进行托管。当然，nginx远不止这点功能，诸如反向代理、缓存、负载均衡等等比较强大的功能。

将生成的静态文件复制到nginx的html目录下即可，不用做任何改动。如果没有服务器，可以在Windows或者使用VMware虚拟机搭建Linux环境安装nginx进行测试。关于nginx入门教程，可以在站内搜索：nginx入门到实践。
访问：http://localhost 或者 http://127.0.0.1，体验还不错。




如果想打造炫酷、实用的hexo静态博客，可以参考这两位的博客，搜索hexo相关优化资料。
- Sukka：https://blog.skk.moe
- zu1k：https://zu1k.com


——END——