---
title: SQL Server连接时出现的连接超时：无其他信息。请验证连接属性。报错的解决方法
date: 2021-03-10 10:35:51
tags:
- SQL Server
---

SQL Server连接时出现如下图的报错

![](1.PNG)

------

解决方法：

1、打开SQLServer的Sql Server Configuration Manager管理配置工具

2、点入“SQL Native Client”（安装的是32位的就点击32位的），再点击“TCP/IP属性”，查看端口号并记下，然后开启“TCP/IP属性”

![](2.png)

![](3.png)

3、点击“SQL Server网络配置”，再点击SQLServer对应的实例协议，再点击“TCP/IP属性”，拉到最下方，看到TCP动态端口，将端口号改为之前在“SQL Native Client”中的端口号，修改后保存并启动“TCP/IP属性”

![](4.png)

4、最后别忘了在“SQL Server服务”中启动对应实例的服务

![](5.png)



以上