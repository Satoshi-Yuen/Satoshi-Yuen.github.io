---
title: MyBatis与Spring的整合
date: 2020-05-24 16:48:08
tags:
- MyBatis
- Spring
---
个人认为，MyBatis与Spring整合后，使得MyBatis框架的作用更为凸显，将数据库的连接工作交给Spring执行，同时也可以提高对整一个项目的清晰度。
以下是整合的六大步骤：
一、整合所需的JAR包
&#8195;MyBatis框架所需的JAR包：
![](m1.JPG)
![](m2.JPG)
![](m3.JPG)
![](m4.JPG)
![](m5.JPG)
![](m7.JPG)
&#8195;Spring框架所需的JAR包：
![](s1.JPG)
![](s2.JPG)
![](s3.JPG)
&#8195;MyBatis与Spring框架整合所需的中间JAR包：
![](ms.JPG)
&#8195;数据库驱动JAR包：
![](db.JPG)
&#8195;数据源所需JAR包：
&#8195;&#8195;&#8195;整合时使用DBCP数据源，所以需要DBCP的JAR包；
![](ds1.JPG)
&#8195;&#8195;&#8195;连接池的JAR包：
![](ds2.JPG)

二、创建持久化类
&#8195;例如：
![](po1.JPG)
![](po2.JPG)
&#8195;&#8195;注意：类中的属性名必须与数据库中的数据表属性名相同。

三、Spring文件配置
&#8195;配置MyBatis工厂
&#8195;&#8195;MyBatis的sqlSessionFactory交由Spring来配置，Spring配置文件applicationContext.xml中添加如下代码（applicationContext.xml文件要在项目的src目录下创建）：
![](sa1.JPG)
&#8195;&#8195;注意：红线内容表示数据库的连接地址；
&#8195;使用Spring管理MyBatis数据操作接口
&#8195;&#8195;Spring配置文件applicationContext.xml中添加如下代码：
![](sa2.JPG)
整一个applicationContext.xml代码：
![](sa.JPG)
![](sa-1.JPG)

四、MyBatis文件配置
&#8195;在项目的src目录下创建一个包，用于存放sql映射文件和MyBatis核心配置文件，例如：
![](mset1.JPG)
&#8195;&#8195;配置sql映射文件，例如：
![](mset2.JPG)
&#8195;&#8195;&#8195;注意：select中的id要与Dao包中的函数名完全一致！
&#8195;&#8195;配置核心文件mybatis-config.xml，例如：
![](mset3.JPG)
&#8195;&#8195;&#8195;注意：这个时候的mybatis-config.xml文件与未整合前的mybatis-config.xml文件有很大区别，整合后的mybatis-config.xml文件只需要配置映射文件地址（sql映射文件）、红线部分需要留意。

五、创建Dao层接口函数
&#8195;第三步的Spring文件配置中的”使用Spring管理MyBatis数据操作接口“就是扫描Dao层中带有@Mapper注解的所有接口函数并装配，而接口访问函数的名称必须与sql映射文件的select的id相一致，也就是第四点MyBatis文件配置中配置sql映射文件的注意事项，Dao层接口访问函数，例如：
![](dao1.JPG)
![](dao2.JPG)

六、创建Controller（控制器）层
&#8195;Controller（控制器）层主要是用于调用数据访问接口方法（功能方法的业务逻辑在Service层中实现，此处没有给出），在Controller（控制器）层当中，需要用@Controller注解标识类供主函数通过控制器可以找到相应的功能函数进行使用，同时，若使用到接口对象或者类对象，需要用@Repository、@Service、@Resource这样的注解联合标识使用（这样的标识在一个类中只能使用一次），或@Autowired注解（可重复使用）进行一一标识，例如：
![](c1.JPG)

MyBatis与Spring的整合的主要步骤阐述结束！
以上。


