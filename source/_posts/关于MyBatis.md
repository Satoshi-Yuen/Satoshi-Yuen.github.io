---
title: MyBatis小入门
date: 2020-04-17 17:10:31
tags:
- Java
- Web开发
- MyBatis
---
这是关于MyBatis的个人入门总结。
&#8195;MyBatis是基于Java的持久型框架，也是一个半自动映射的框架，它消除了几乎所有的JDBC代码和参数的手工配置以及结果集的检索，主要是用XML或者注解的形式配置和原始映射，将接口和POJOs（普通的Java对象）映射成数据库中的记录。
MyBatis工作原理：
&#8195;（1）读取MyBatis配置文件：mybatis-config.xml为MyBatis的全局配置文件，有数据库连接等的运行环境的信息；
&#8195;（2）加载映射文件：指的是加载SQL映射文件，文件中配置了相关的SQL语句，也需要在mybatis-config.xml中配置，每一个映射文件对应一张数据库的表；<!--more-->
&#8195;（3）构造会话工厂：通过MyBatis的配置信息构建会话工厂SqlSessionFactory；
&#8195;（4）创建会话对象：会话工厂创建SqlSession对象，此对象包含执行SQL语句的所有方法；
&#8195;（5）Executor执行器：这是用来操作数据库的接口，根据SqlSession传递的参数动态地生成需要执行的SQL语句；
&#8195;（6）MappedStatement对象：这是Executor接口执行方法的一个参数，是对映射信息的封装，用来存储要映射的SQL语句的id、参数等；
&#8195;（7）输入参数映射：类似于JDBC对preparedStatement对象设置参数的过程；
&#8195;（8）输出参数映射：类似于JDBC对结果集的解析过程；

&#8195;&#8195;一般的MyBatis框架按上面的步骤搞就差不多了，当然，也可以将Spring和MyBatis揉在一起，至于为什么要揉在一起，图的就是方便，怎么柔在一块呢，接着看看：
&#8195;原来的mybatis-config.xml只做一个数据库表的映射，数据库配置/指定数据源、事务管理、MyBatis接口扫描等等的配置则扔到Spring的applicationContext.xml里

&#8195;&#8195;有些人可能会bb，揉在一起也还是要写配置，还是麻烦；其实还有操作可以节省配置的时间，是什么呢，接着来看我喷口水：
&#8195;可以使用MyBatis的Generation插件来自动生成映射文件，这个插件可以自动生成MyBatis需要的DAO接口、实体模型类、Mapping映射文件。
操作步骤：
&#8195;（1）准备jar包：mysql-connect-java-版本号-bin.jar和mybatis-generator-core-版本号.jar；
&#8195;（2）创建文件夹：随便在一个盘里创个文件夹，把上面的jar包扔进来，再在这个文件夹里再传一个文件夹放生成的相关代码文件；
&#8195;（3）创建配置文件：在根文件夹创建一个xml文件，配置内容请百度；
&#8195;（4）生成代码文件：打开电脑的cmd，进入到你创建的那个文件夹（根目录，不是存代码的那个），输入命令：java-jar mybatis-generator-core-版本号.jar -configfile (你创建的xxx.xml文件)-overwrite;
&#8195;生成的代码文件就在存代码的文件夹里，当然，这个只是生成一个模板一样的东西，里面详细的内容还是需要你来配置的~。

以上。
