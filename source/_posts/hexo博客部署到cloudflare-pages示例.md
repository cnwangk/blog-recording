---
title: hexo博客fluid主题部署到cloudflare pages示例
date: 2023-05-05 00:13:46
tags: hexo
categories:
- 静态博客
---

先上demo示例效果： 
- 体验地址：https://demo.cnwangk.top/ 
- 备用地址：https://blog-wangk-demo.pages.dev/


**cloudflare pages 支持部署方式**

- 连接至git：支持从 github & gitlab 仓库导入 cloudflare pages。
- 直接上传：支持手动上传压缩包以及文件 cloudflare pages，直接上传可能会出现中文目录乱码（需要统一编码为：utf-8，否则大概率中文乱码）。
- Wrangler CLI：支持wrangler cli 推送项目到 cloudflare pages，个人推荐这种方式或者链接 github 仓库。

<!-- more -->


**示例：Wrangler CLI 创建项目**
使用 Wrangler CLI 创建项目，利用 Wrangler 命令行界面 (CLI) 创建和部署站点。

1. npm install -g wrangler
2. wrangler login
3. npx wrangler pages publish 接项目（生成静态资源文件）所在目录
4. 选择新建项目或者推送已有项目

具体操作如下：

```bash
[root@localhost blog]# npx wrangler pages publish public/   #推送项目
No project selected. Would you like to create one or use an existing project?
  Create a new project      # 创建新项目
❯ Use an existing project   # 使用已有项目
Select a project:           # 选择已有项目
❯ blog-wangk-demo
  blog-wangk-hexo
  blog-wangk-hugo
  blog-wangk-jekyll
🌍  Uploading... (280/280)

✨ Success! Uploaded 0 files (280 already uploaded) (1.82 sec)

✨ Deployment complete! Take a peek over at https://05f68913.blog-wangk-demo.pages.dev
```

输出：看到 Success! Uploaded 代表上传资源成功。



—END—

