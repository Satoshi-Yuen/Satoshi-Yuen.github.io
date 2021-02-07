---
title: org.apache.jasper.compiler.JDTCompiler findType报错
date: 2021-01-27 22:22:56
tags:
- jdk
- Tomcat
---

实习时在搭建开发环境所出现的**org.apache.jasper.compiler.JDTCompiler findType**的报错

原因：由于Tomcat版本过低或jdk版本过高的不协调导致的错误（笔者使用的是v9的tomcat和1.8的jdk）

解决办法：降低jdk版本或提升tomcat版本；

由于tomcat版本够高，所以笔者就降低了jdk版本至1.7

紧接着，问题就解决了



以上