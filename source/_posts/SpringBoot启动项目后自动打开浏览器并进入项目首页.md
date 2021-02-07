---
title: SpringBoot启动项目后自动打开浏览器并进入项目首页
date: 2021-02-07 23:08:44
tags:
- SpringBoot
---

实现方式因人而异，题主是放在主类中实现：

```java
String url = "http://localhost:8080/";
Runtime runtime = Runtime.getRuntime();
try {
    runtime.exec("rundll32 url.dll,FileProtocolHandler " + url);
    System.out.println("启动浏览器成功，进入index首页...");
} catch (IOException e) {
    e.printStackTrace();
}
```

代码源于网络



以上