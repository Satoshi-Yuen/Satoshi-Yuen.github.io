---
title: Eslint&Git&哈士奇
date: 2020-05-05 16:32:07
tags:
- git
- Eslint
- husky
---
Eslint：JavaScript代码检查工具；
使用步骤：
（1）确保电脑上已安装node与npm环境；
（2）创建项目：npm init；
（3）本地安装：npm install eslint &#8211;&#8211;save&#8211;dev；
（4）设置package.json文件，在文件内添加以下内容：
![](1.JPG)<!--more-->
哈士奇（husky）：一个将git和eslint结合起来的库,为git创建钩子（hooks），解决代码风格之间产生的冲突；
安装步骤：
（1）创建一个git工作目录；
（2）在工作目录下，npm install husky &#8211;&#8211;save&#8211;dev命令进行安装；
（3）在package.json文件中添加以下内容：
![](2.JPG)
