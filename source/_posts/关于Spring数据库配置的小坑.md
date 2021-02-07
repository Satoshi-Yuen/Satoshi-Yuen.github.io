---
title: 关于Spring数据库配置的小坑
date: 2020-04-12 15:32:17
tags:
- Java
- SpringJDBC
---
Java使用注解配置MySQL信息报错：
第一个坑：
![](keng1.jpg)
解决方案：
![](pokeng1.jpg)
已上图为例，在utf8后面接上&amp；serverTimezone=UTC

第二个坑：
![](keng2.jpg)
对实体“xxx”的应用必须以“；”分隔符结尾
解决方案：
例如数据库url是这样的：
![](pokeng2.jpg)
将'&'改写为”&amp；“,即jdbc:mysql://localhost:3306/xsgl?charaterEncoding=utf8&amp；serverTimezone=UTC



最近在学习SpringBoot时，配置数据库时遇到的类似bug：

1、**<u>Loading class `com.mysql.jdbc.Driver'. This is deprecated. The new driver class is `com.mysql.cj.jdbc.Driver'. The driver is automatically registered via the SPI and manual loading of the driver class is generally unnecessary.</u>**

**原因：**6版本后的mysql驱动类，Driver位置由com.mysql.jdbc.Driver 变为com.mysql.cj.jdbc.Driver
**解决方式：**将数据配置文件的spring.datasource.driver-class-name=com.mysql.jdbc.Driver改为spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver



2、**<u>Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn't set.</u>** 

**解决方式：**加上useSSL=false并且设置上时区



3、**<u>Could not retrieve transation read-only status server</u>**

**原因：**mysql-connector-java依赖版本与mysql版本号不对应

**解决方式：**更换为mysql版本所对应的版本号