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
