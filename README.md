# 个人博客源码仓库

我尽可能详细说明，希望小白（新入坑）人群看到也能轻松上手。个人每隔一段时间，会输出一堆垃圾博文。

采用 [hexo](https://hexo.io/) 和 [next](https://theme-next.js.org/) 主题打造。如果你想和我一样打造一款属于自己的博客站点，需要做如下操作。

主站和主题配置说明，尽本人最大能力去解释说明。配置文件（站点根目录）：

| 文件             | 作用            |
| ---------------- | --------------- |
| _config.yml      | hexo 主站点配置 |
| _config.next.yml | next 主题配置   |



### 疑惑解答

为什么要部署  [Git](https://git-scm.com/download/win)  环境？

答：主要用于版本控制，将生成的静态资源文件推送到 github 、gitee 等支持代码托管以及 pages 服务的平台。



为什么要部署  [nodejs](https://nodejs.org/zh-cn)  环境？

答：主要用于安装静态博客生成器需要的依赖包，包含需要使用到的 npm 工具。

推荐使用国内 npm 镜像源地址。如何配置，请参考个人这篇博文： [npm切换镜像源](https://blog.cnwangk.top/2023/03/26/npm切换镜像源/)



为什么要部署  [hexo](http://hexo.io/zh-cn/) 环境？

> Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他标记语言）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

答：主要用于生成静态博客网站框架页面（ html + js + css + xml ）文件。



为什么要部署  [next](https://github.com/next-theme/hexo-theme-next) 主题环境？

答：主要用于生成静态博客主题页面（ html + js + css + xml ）文件。不限于 next 主题，可以使用你喜欢的主题。



### 仓库目录

本仓库目录作用说明：

1. `.deploy_git` 目录：存放带有 git 版本控制的静态资源目录，需要部署 [hexo-deployer-git](https://hexo.io/docs/one-command-deployment) 插件。
2. node_modules 目录：存放 npm 工具安装的依赖文件。
3. public 目录：与 `.deploy_git` 类似，存放 `hexo g` 生成后的静态资源文件。
4. scaffolds 目录：存放模板文件。
5. source 目录：存放网站源码文件。
6. themes 目录：存放站点主题文件。
7. _config.yml 文件：hexo 站点配置文件。
8. _config.next.yml 文件：next 主题配置文件。
9. package.json：保存 npm 安装插件版本的信息文件。
10. `.gitignore`：git 版本控制忽略提交推送哪些文件，拆解单词  git  ignore 。



**scaffolds 目录作用说明**：

| 目录     | 作用             |
| -------- | ---------------- |
| draft.md | 草稿文件模板     |
| page.md  | 目录页面文件模板 |
| post.md  | 博文文件模板     |



**source 目录作用说明**：

| 目录             | 作用                                                         |
| ---------------- | ------------------------------------------------------------ |
| _data            | 数据（比如利用相关插件生成的 json 数据文件）目录             |
| _posts           | 博文生成目录                                                 |
| about            | 关于（自我简介）目录                                         |
| categories       | 类别目录                                                     |
| tags             | 标签目录                                                     |
| images           | 图片目录                                                     |
| links            | 个人自定义友情链接目录（你也可以定义为 friends）             |
| happy            | 个人自定义娱乐项目目录                                       |
| BingSiteAuth.xml | SEO：在必应搜索引擎进行提交站点信息                          |
| CNAME            | 解析域名形式，使用某些插件需要在 source 目录加上 CNAME 配置文件 |



### 环境搭建


必备（部署）环境：

1. [git](https://git-scm.com/download/win) & [nodejs](https://nodejs.org/zh-cn)
2. 部署 [hexo](http://hexo.io/zh-cn/) 静态博客生成器：`npm install hexo-cli -g`
3. 安装 [next](https://github.com/next-theme/hexo-theme-next) 主题：`npm install hexo-theme-next`



hexo 部署步骤：

```bash
npm install hexo-cli -g   #1.部署 hexo 客户端工具（-g ， 全局模式）
hexo init blog			  #2.初始化 blog 站点目录（存放站点配置文件以及资源文件）	
cd blog					  #3.进入 blog 目录
npm install               #4.安装依赖
hexo server				  #5.启动 hexo 服务
```



next 主题部署方式（两种）

- 方式一，利用 hexo 5.x 以及更高版本的特性，推荐使用 npm 工具直接部署 ：`npm install hexo-theme-next` ，主题部署目录保存在 blog 目录中  node_modules\hexo-theme-next  。
- 方式二，利用 Git 工具部署：`git clone https://github.com/next-theme/hexo-theme-next themes/next` ，正常部署 hexo 会生成  themes 目录，将 next 主题克隆到 themes  中，好处是可以直接利用 git 做版本控制。

方式一部署步骤：

```bash
$ mkdir blog-hexo-site      		#1.建立博客站点工作空间
$ cd blog-hexo-site					#2.进入站点工作空间
$ npm install hexo-theme-next		#3.部署 next 主题
$ cp .\node_modules\hexo-theme-next\_config.yml  .\_config.next.yml  #4.复制主题配置文件到当前站点目录
```

方式二部署步骤：

```bash
$ mkdir blog-hexo-site
$ cd blog-hexo-site
$ git clone https://github.com/next-theme/hexo-theme-next themes/next
```



hexo 主站加入配置：

```yml
theme: next
```



更详细的部署方式以及目录说明请参考 [hexo](http://hexo.io/zh-cn/) 文档站和  [next](https://github.com/next-theme/hexo-theme-next)  主题仓库。



正常部署，可以查看到工具版本信息：

```bash
node -v  #查看nodejs版本
v16.18.1
npm -v   #查看 npm 工具版本
8.19.2
hexo -v  #查看 hexo 相关连工具版本 
INFO  Validating config
hexo: 6.3.0  			#hexo版本
hexo-cli: 4.3.0			#hexo客户端版本
os: win32 10.0.22000    #操作系统版本
node: 16.18.1		    #nodejs版本	
v8: 9.4.146.26-node.22
uv: 1.43.0
zlib: 1.2.11
brotli: 1.0.9
ares: 1.18.1
modules: 93
nghttp2: 1.47.0
napi: 8
llhttp: 6.0.10
openssl: 1.1.1q+quic
cldr: 41.0
icu: 71.1
tz: 2022b
unicode: 14.0
ngtcp2: 0.8.1
nghttp3: 0.7.0
```



如果你直接 git clone 了我的仓库，需要做如下操作：

1. 部署 [nodejs](https://nodejs.org/zh-cn) 环境
2. 部署 hexo 客户端工具：`npm install hexo-cli -g`
2. 安装依赖： `npm install`
3. 启动服务：`hexo s`
4. 访问站点：[http://127.0.0.1:4000/](http://192.168.0.233:4000/)



### 效果展示

![https://s1.ax1x.com/2023/06/25/pCNWta9.png](https://s1.ax1x.com/2023/06/25/pCNWta9.png)



效果展示，在线地址：

1. **备用地址**：
   - [https://blog.cnwangk.top/](https://blog.cnwangk.top/)
     - 部署在 vercel：[https://vercel.com/](https://vercel.com/)
   - [https://www.cnwangk.top/](https://www.cnwangk.top/)
     - 部署在 netlify：[https://app.netlify.com/](https://app.netlify.com/)
   - [https://cf.cnwangk.top/](https://cf.cnwangk.top/)
     - 部署在 cloudflare：[https://dash.cloudflare.com/](https://dash.cloudflare.com/)
   
2. 主站地址：
   - [https://wzgy.cnwangk.top/](https://wzgy.cnwangk.top/)
     - 部署在github：[https://github.com/cnwangk/cnwangk.github.io](https://github.com/cnwangk/cnwangk.github.io)



### 注意事项

next 主题仓库相关，一共有三个仓库：

| 版本            | 年份        | 仓库                                                         |
| --------------- | ----------- | ------------------------------------------------------------ |
| v5.1.4 或更低   | 2014 ~ 2017 | [https://github.com/iissnan/hexo-theme-next](https://github.com/iissnan/hexo-theme-next) |
| v6.0.0 ~ v7.8.0 | 2018 ~ 2019 | [https://github.com/theme-next/hexo-theme-next](https://github.com/theme-next/hexo-theme-next) |
| v8.0.0 或更高   | 2020 ~ 至今 | [https://github.com/next-theme/hexo-theme-next](https://github.com/next-theme/hexo-theme-next) |

1. [next 5.x](https://github.com/iissnan/hexo-theme-next) ，仓库很长一段时间没更新，不推荐使用。
2. [next 6.x ~ 7.x](https://github.com/theme-next/hexo-theme-next)  ，仓库很长一段时间没更新，不推荐使用。
3. [next 8.x](https://github.com/next-theme/hexo-theme-next)（个人当前使用版本 v8.16.0），**推荐使用**。

引用 next 8.x 主题仓库一篇 issues 的 一段说明：

> 遗憾的是，每个新仓库的创建者都没有 Archive 旧仓库的权限，导致了历史遗留问题。为了避免安装过时的 NexT 版本，请务必按照本仓库 README 中提供的几种安装方式进行操作。
> 跨版本的升级可能并不顺滑（例如由 v5.1.4 或 v7.8.0 升级至 v8.0.0），请备份配置文件及修改过的文件（例如自定义模板文件）后，重新安装新的主题。具体操作请阅读文档： https://theme-next.js.org/docs/getting-started/upgrade.html



详情请戳这篇 issues ，**必读更新说明及常见问题**：

[https://github.com/next-theme/hexo-theme-next/issues/4](https://github.com/next-theme/hexo-theme-next/issues/4)



# 絮絮叨叨 END

静下心来，才发现原来不会的还有很多。

一分耕耘，一分收获。

多总结，你会发现，自己的知识宝库越来越丰富。



如果你有幸看到这个仓库，希望对你的学习和工作有所帮助哟！



# 感谢

感谢这些平台提供友好的服务支持，我才可以愉快的打造个人博客站点。

- [github pages](https://pages.github.com/)
- [hexo](https://hexo.io/) & [hexo-theme-next](https://theme-next.js.org/)
- vercel：[https://vercel.com/](https://vercel.com/)
- netlify：[https://app.netlify.com/](https://app.netlify.com/)
- cloudflare：[https://dash.cloudflare.com/](https://dash.cloudflare.com/)



**—END—**  