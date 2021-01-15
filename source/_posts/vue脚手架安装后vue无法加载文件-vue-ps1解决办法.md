---
title: vue脚手架安装后vue无法加载文件"...\vue.ps1"解决办法
date: 2021-01-15 18:28:10
tags:
- vue
---

这是在vscode中安装好Vue-CLI后运行vue命令时出现的报错，如下图：

![](捕获.PNG)

**解决方法：**

以管理员的身份运行windows PowerShell（一定要以管理员身份运行），然后输入命令set-ExecutionPolicy RemoteSigned，输入Y后确定：

![](2.PNG)

再看vscode，问题迎刃而解：

![](3.PNG)



以上