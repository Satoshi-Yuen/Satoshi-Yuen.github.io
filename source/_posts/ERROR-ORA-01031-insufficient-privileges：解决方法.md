---
title: 'ERROR: ORA-01031: insufficient privileges：解决方法'
date: 2021-02-07 22:16:50
tags:
- oracle
- PLSQL
---

这是在配置PLSQL时出现的问题：

## ERROR: ORA-01031: insufficient privileges：

1、首先win+R打开compmgmt.msc

![](1.png)

2、找到“本地用户和组”，然后进入“组”，寻找是否有ora_dba

![](2.png)

3、若有，进入“用户”，找到自己的用户，一般是第一个，点击进入

![](3.png)

4、找到“隶属于”，然后点击下方的“添加”

![](4.png)

![](5.png)

5、再点击“高级”，然后点击“立即查找”

![](6.png)

6、等待查找结束后，选中名称为“ora_dba”的然后一路点击“确定”就完事了

![](7.png)



以上