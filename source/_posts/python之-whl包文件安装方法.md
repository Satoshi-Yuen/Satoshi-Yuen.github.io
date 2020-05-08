---
title: python之.whl包文件安装方法
date: 2020-05-08 11:25:48
tags:
- Python
---
直入正题：
实行这个方法的前提是确保已经安装pip工具！
python的模块包下载网址：https://www.lfd.uci.edu/~gohlke/pythonlibs/ 
这个网站提供相关的python模块包下载，都比较齐全。
以下载pandas包为例进行步骤讲解：
（1）根据个人需要下载好.whl包文件；
（2）将下载好的.whl包文件放入pip安装的目录下，个人放的是python解释器下的Scripts文件夹，其实绝大数人也是；
（3）以管理员身份运行cmd并一路cd到你的包文件所放入的文件夹下（Scripts文件夹下），如图：
![](1.JPG)
（4）输入命令：pip install pandas-0.25.3-cp38-cp38-win_amd64.whl，如图：
![](2.JPG)
这样就安装成功！

以上
