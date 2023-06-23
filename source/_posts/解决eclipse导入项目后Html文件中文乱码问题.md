---
title: 解决eclipse导入项目后Html文件中文乱码问题
date: 2017-06-26 
tags: eclipse
categories: 
- [开发工具]
---

几年前，刚毕业不久，接触到eclipse for JavaEE开发工具，当时不知道默认编码为GBK，或者是ISO-8859-1。

解决eclipse导入项目后Html文件中文乱码问题，修改字符编码，主要是修改html文件的编码。

### 一、修改workspace的默认编码
1. 依次找到：windows->General->Workspace
2. 全局生效：将 Text file encoding 的other选项改为 UTF-8


### 二、修改Resource默认字符编码

1. 单项目生效：右键项目找到Text file encoding
2. 将other选项改为 UTF-8



### 三、解决方案


依次找到路径：

1. windows->perferences->General->Content Types->Text->HTML
2. 然后将Default encoding设置为UTF-8即可。



——END——

 