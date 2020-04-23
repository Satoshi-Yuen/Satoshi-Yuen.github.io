---
title: 构建基础的hexo博客框架
date: 2020-04-13 01:01:19
tags:
- hexo
- hexo博客框架
---
&#8195;&#8195;许多人在学习的时候都会做下笔记，忘记的时候可以看看，温故而知新，而很多人都想着在博客上写，记录不止是知识，还有点滴，同时也有人想搭建一个自己的博客（感觉很酷，顺带也可以装逼），以hexo博客框架为基础的博客就十分友好地诞生了！搭建简单，而且后期也容易维护，小鲜肉我在各路搜索资料搭建好后，总结出了些些心得，现在就开始简单地喷下口水：
小鲜肉本人使用的是windows系统，所以都是基于windows来搭建：
（1）下载node.js
&#8195;下载网址：nodejs.org
&#8195;默认选项安装，安装好后可以打开cmd，使用node -v查看版本号(npm -v查看包管理器的版本)。
（2）下载git
&#8195;到git官网去下载windows版本就OK啦，安装的时候可以默认选项安装，当然，你也可以选择，毕竟萝卜青菜各有所爱。<!--more-->
（3）镜像源安装
&#8195;（至于这个是干嘛用的的呢，自行百度吧，这里就不吹水了），用npm安装cnpm：npm insatll -g cnpm –registry=http://registry.npm.taobao.org，安装好了可以用cnpm、cnpm -v查看相关信息。
（4）建文件夹
&#8195;在电脑中建立一个文件夹用来存放关于博客的文件的文件夹，文件夹右键点击git bash here，进入到git，或者也可以先进入git bash然后在建立文件夹（博客的所有操作都在git bash上进行）。
（5）安装hexo博客框架
&#8195;命令：cnpm install -g hexo -cli（hexo -v查看hexo框架的相关信息）。
（6）初始化博客
&#8195;命令：hexo init，初始化之后会显示http://localhost:4000，在浏览器上输入localhost:4000即可查看搭建的hexo博客原始形态。

&#8195;&#8195;到了这个地步，基本框架就已经搞定了，可以启动博客（hexo s）开始写博客（hexo n “article title”），在hexo n之后，会帮你在/source/带下划线的posts中创建一个”article title”.md的文件，用vim打开来写就完事了。
不过你写完上传到博客，因为你的博客只是供本地浏览，别人是不知道你写了什么鬼，也不知道你有博客（进而无法装逼），如果你想着自娱自乐，那可以关掉这篇博客写你的博客，如果想装逼，可以接着看我吹水：

将博客部署到Github（全球最大的同性交友网站），重要的是此举免费，免费，免费：
（1）注册Github账号
&#8195;必须得有，没有去搞，说完。
（2）创建一个repository
&#8195;关键步骤：repository name一栏的填写格式：账号昵称+.github.io，勾选“Initialize this repository with a README”，点确认，完事。
（3）安装git插件：
&#8195;在你的blog文件夹下部署一个git的插件，主要是将你博客文件夹的东西扔到repository里，命令：cnpm insatll –save hexo-deployer-git
（4）改内容
&#8195;在你创建的blog文件夹下，有一个带下划线config.yml的文件，vim打开，拖到文件底部，找到Deployment，补充以下内容：
&#8195;&#8195;type：git
&#8195;&#8195;repo：创建的repository地址
&#8195;&#8195;branch：master
（5）身份验证
&#8195;这个好理解啊，你通过git进入repository肯定要查你身份证啊，所以这个时候你执行部署到github上的命令（hexo d）时，会弹出一个status的验证，你需要输入一下命令进行验证：
&#8195;&#8195;git config –global user.email “github账号绑定的邮箱”
&#8195;&#8195;git config –global user.name “github账号的昵称”
&#8195;完成验证后，再次输入hexo d进行部署，部署完后回到github的repository，点击code，就会看到无端端多了团东西，那是博客文件夹里的东西。

好了，部署到Github上的步骤就告一段落了~
但是，你以为完了吗，其实差不多完了，容我在喷多些口水：
&#8195;在浏览器上输入你的仓库名（”账户昵称+.github.io”），就可以访问到你部署到github的博客，其他人输入你的仓库名也就可以看到你的博客，成功装逼，要是你嫌这个仓库名太low，没关系，花些小钱买个域名进行装逼升华，何乐而不为！
另外，有些朋友在克隆时可能会遇到以下问题：
![](clonefalse.jpg)
一般提升缓存就完事了，命令如下：git config –global http.postBuffer +缓存大小

&#8195;口水喷完了，打游戏去了，至于你看到你的博客为什么还是空空如也，自己耍去吧
&#8195;以上。
