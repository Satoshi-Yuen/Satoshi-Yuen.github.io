---
title: 安装与更换jdk
date: 2021-02-07 22:37:41
tags:
- jdk
---

## 安装与更换jdk

### 安装jdk：

1、到官网（

[https://www.oracle.com/cn/java/technologies/javase-downloads.html]: 

）上下载jdk；

2、傻瓜安装，安装路径因人而异；

3、创建环境变量

JAVA_HOME：jdk的安装路径

CLASSPATH：.\;%JAVA_HOME%\lib\dt.jar;\%JAVA_HOME%\lib\tools.jar;%JAVA_HOME%\bin

path：%JAVA_HOME%\bin;

### 更换jdk：

1、将bin文件夹下的java、javaw、javaws文件夹复制放入**C:\ProgramData\Oracle\Java\javapath**和**C:\Windows\System32**下，覆盖原来的java、javaw、javaws；本质上就是覆盖原来的jdk。

2、修改注册表（未亲测）

先使用快捷键组合win+R进入redirect（进入注册表编辑器）：

![](1.png)

接着按照以下图示一步一步操作找到JavaSoft文件夹下的Java Development Kit文件夹并修改CurrentVersion的数据为更换的jdk版本，如1.8：

![](2.png)

![](3.png)

![](4.png)

然后找到下面的Java Runtime Environment文件夹，也是修改CurrentVersion的数据值为更换的jdk版本，如1.8

![](5.png)



完成，以上