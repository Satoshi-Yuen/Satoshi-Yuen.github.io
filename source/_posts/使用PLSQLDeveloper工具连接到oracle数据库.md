---
title: 使用PLSQLDeveloper工具连接到oracle数据库
date: 2021-02-07 23:00:49
tags:
- PLSQL
- oracle
---

首先确保oracle安装成功

接着：

1、环境变量配置：

ORACLE_HOME：V:\PLSQL\PLSQL\instantclient_11_2（PLSQLDeveloper的instantclient_11_2文件夹路径）
TNS_ADMIN：V:\PLSQL\PLSQL\instantclient_11_2（PLSQLDeveloper的instantclient_11_2文件夹路径）
NLS_LANG：SIMPLIFIED CHINESE_CHINA.ZHS16GBK 
path：V:\PLSQL\PLSQL\instantclient_11_2（PLSQLDeveloper的instantclient_11_2文件夹路径）

2、进入PLSQLDeveloper

3、“工具”->“首选项”，看到oracle下的“连接”，将ORACLE主目录设置为instantclient_11_2文件夹所在路径，OCI库配置为instantclient_11_2文件夹下oci.dll文件的路径

![](1.png)

4、将oracle安装路径下\product\11.2.0\dbhome_1\NETWORK\ADMIN的tnsnames.ora文件复制移动到PLSQL安装目录下的instantclient_11_2文件夹内



以上