---
title: SpringBoot基础(一)
date: 2021-01-03 22:18:07
tags:
- SpringBoot
---
以下是在学习SpringBoot过程中的笔记

SpringBoot：整合Spring技术栈的一站式框架，简化Spring技术栈的快速开发脚手架

## 一、初始化

创建maven项目，配置pom文件和注入依赖（官方文档）；
在主类上添加注释@SpringBootApplication：告知这是一个SpringBoot应用；
@RestController=@Controller+@ResponseBody：注释放在Controller类中；
关于依赖管理：
父项目依赖管理：几乎声明所有开发中要用的依赖的版本号；
场景启动器：引入starter这个场景的所有常规都会自动引入；
以上均在pom文件中配合，官方文档有源码



## 二、自动配置

1、自动配置好Tomcat；
2、自动配置好SpringMVC
&#8195;引入SpringMVC全套组件；
&#8195;自动配置好SpringMVC常用组件；
3、自动配置好web常用功能；
4、默认包结构
&#8195;主程序所在包及其下面所有子包的组件都会被扫入；
&#8195;扫入不在主程序所在包的其他包，注释配置：@SpringBootApplication(scanBasePackages="路径")；或@ComponentScan("路径")：指定扫描路径；
5、各种配置都有默认值
&#8195;配置文件的值最终绑定到每个类上，这个类会在容器中创建对象；
6、按需加载自动配置



## 三、底层注解

1、@Configuration(proxyBeanMethods=true/false)：告诉SpringBoot是一个配置类（相当于是spring原生中的xml配置文件），并且SpringBoot会检查这个组件是否在容器当中；
&#8195;（1）给容器中添加组件，以方法名作为组件id，返回类型是组件类型，返回的值是组件在容器中实例
&#8195;&#8195;*外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的实例对象；
&#8195;&#8195;*配置类里面使用@Bean注释标注在方法上给容器注册组件，默认是单实例，配置类本身也是组件；
&#8195;（2）proxyBeanMethods：代理bean方法，参数选择：
&#8195;&#8195;true：类组件之间有依赖关系方法调用得到之前单实例组件；
&#8195;&#8195;false：类组件之间无依赖关系，类组件之间有依赖关系方法调用得到新的实例；
2、@Import(...,...)：导入组件，给容器中自动创建出两个类型的组件，默认组件名是全类名；
3、@Conditional：条件装配，满足Conditional指定的条件则进行组件注入；
&#8195;@ConditionalOnBean(name="xxx")：当有名为xxx的组件时才会执行怎样的操作；
&#8195;@ConditionalOnMissingBean(name="xxx")：当没有名为xxx的组件时才会执行怎样的操作；
4、@ImportResource()：导入Spring配置文件，classpath:.....xml；
5、@ConfigurationProperties：配置绑定，只有在容器中的组件，才会有SpringBoot提供的功能；
&#8195;@ConfigurationProperties+@Component：Dao类上配置；
&#8195;@EnableConfigurationProperties(....class)+@ConfigurationProperties：在配置类上配置，参数为Dao类名.class；



## 四、自动配置原理

引导加载自动配置类
1、@SpringBootConfiguration
&#8195;@Configuration：代表当前是一个配置类；
2、@ConponentScan：扫描包；
3、@EnableAutoConfiguration；
&#8195;*@SpringBootApplication=@SpringBootConfiguration+@ConponentScan+@EnableAutoConfiguration；
4、@AutoConfigurationPackage：利用Registrar给容器中导入一系列组件，将指定的一个报下的所有组件导入；
总结：
（1）SpringBoot先加载所有自动配置类；
（2）每个自动配置类按照条件进行生效，默认都会绑定配置文件指定值；
（3）生效的配置类就给容器中装配很多组件；
（4）只要容器中有这些组件，相对于功能就有了；
（5）定制化配置，用户直接可用自己的@Bean配置替换底层的组件；
&#8195;文件寻找路径：xxxAutoconfiguration-->组件-->xxxProperties中取值-->application.properties



## 五、Spring最佳实践

1、引入场景依赖（starter）；
2、查看自动配置：引入场景对应的自动配置一般都会生效；
3、是否需要修改，修改方式：
&#8195;（1）参照文档修改配置项；
&#8195;（2）自定义加入或者替换组件：@Bean、@Component；
&#8195;（3）自定义xxxcustomizer；
4、Lombok简化开发：引入lombok可以减少bean类相关代码的编写，提高开发效率，实现步骤：
&#8195;（1）pom文件引入相关依赖；
&#8195;（2）在idea中引入lombok插件；
引入lombok后，bean类可以注释来代替某些代码编写：
&#8195;&#8195;@Data：自动写get/set方法；
&#8195;&#8195;@ToString：自动写toString方法；
&#8195;&#8195;@AllargsConstructor：全参构造函数，自动构造；
&#8195;&#8195;@NoargsConstructor：无参构造函数，自动构造；
5、dev-tools：热更新；
&#8195;通过pom文件配置相关依赖，引入后，只要Ctrl+F9就可不用重启项目，实现实时更新；
6、Spring Initailizar：项目初始化向导，相当于是创建项目时把需要的场景选上，然后就会自动配置完成



## 六、yaml

yaml，标记语言，相当于properties，基本语法：
（1）key: value（键值对，冒号后有一空格）；
（2）区分大小写；
（3）使用缩进表示层级关系；要点：
&#8195;缩进只允许空格，不能使用tab，缩进空格数不限，只要相同层级的元素左对齐即可；
（4）"#"表示注释；
（5）双引号不会转义（有"\"相当于转义，转义再转义相当于不转义），单引号会转义（有"\"，相当于没变化，也就是已转义）；



## 七、静态资源规则与定制化

静态资源目录：/static、/public、/resources、/MEIA-INF/resources；
欢迎页功能：在静态资源路径下的index.html会自动显示，Controller能处理/index请求；要点：
&#8195;静态资源访问路径前缀会影响欢迎页功能，导致不会默认显示；静态资源访问路径前缀在application.yml中配置：
&#8195;&#8195;&#8195;mvc:
&#8195;&#8195;&#8195;&#8195;&#8195;static_path_pattern:/res/xxx;
&#8195;可配置静态资源路径，也是在application.yml中配置：
&#8195;&#8195;&#8195;resources：
&#8195;&#8195;&#8195;&#8195;&#8195;static_locations:classpath:/xxx/xxx;
自定义Favicon：网站小图标，要点：
&#8195;图标的图片名一定要是favicon；
&#8195;同样不能配置静态资源访问路径前缀，导致不会默认显示，但可配置静态资源路径；
&#8195;浏览器缓存也会影响favicon的显示；



## 八、请求处理的常用参数注解

1、@PathVariable("路径中的变量名")：获取路径变量；
2、@RequestHeader("请求头中的变量名")：获取请求头的信息，不加变量名就获取所有请求头信息；
3、@RequestParam("参数名")：获取请求参数（也就是路径中？后面的参数），不加参数名就是获取所有的参数值；
4、@CookieValue("Cookie中某个参数名")：获取cookie值；
5、@RequestAttribute("xxx")：获取request域属性（request.setAttribute中设置的xxx参数名）；
6、@RequestBody：获取请求体信息(post)；



## 九、矩阵变量：@MatrixVariable与UrlPathHelper

矩阵变量形式：/xxx/xxx;k1=v;k2=v1,v2.../xxx;k1=v;k2=v1,v2...;，解析：
&#8195;/xxx/xxx：路径名；
&#8195;k1=v;k2=v1,v2...：矩阵变量；
由于SpringBoot默认禁用矩阵变量，要使用是需要在配置类中配置如下程序：

```java
public WebMvcConfigurer webMvcConfigurer(){
    return new WebMvcConfigurer(){
        @override
        public void configurePathMatch(PathMatchConfigurer configurer){
            UrlPathHelper urlPathHelper=new UrlPathHelper();
            urlPathHelper.setRemoveSemicolonContent(false);
            configurer.setUrlPathHelper(urlPathHelper);
        }
    };
}
```



## 十、视图解析

SpringBoot不支持jsp，需要另一种视图解析器；
thymeleaf视图解析器，语法与jsp类似，要点：
&#8195;使用thymeleaf时要添加starter；
&#8195;在html资源上的html标签要添加模板解析："xmlns:th="http://www.thymeleaf.org""；
另外，关于静态资源，要点：
&#8195;静态资源放在templates文件夹下；



## 十一、拦截器

拦截器主要用于登录检查
主要是实现HandlerInterceptor接口：
&#8195;preHandle：主要是检查登录用户是否为空，空拦截（false），非空不拦截（true）；
&#8195;postHandle
&#8195;afterCompletion
拦截器要点：
&#8195;1、拦截器要配置注册到容器当中，代码模板如下（在配置类中配置）：

```java
public class 类名 implements WebMvcConfigurer{
    @Override
    public void addInterceptors(InterceptorRegistry registry){
        registry.addInterceptor(new 拦截器名()).addPathPatterns("/**").excludePathPatterns("不拦截的资源路径名","不拦截的资源路径名");
    }
}
```

&#8195;代码注意：
&#8195;&#8195;"/**"：表示拦截所有；
&#8195;&#8195;excludePathPatterns表示哪些资源不拦截，多数是静态资源；
&#8195;2、拦截器会拦截所有静态资源；



## 十二、文件上传

要点：
&#8195;1、可使用multiple来标识为多文件上传；
&#8195;2、单个文件上传最大大小：spring.servlet.multipart.max-file-size=大小；
&#8195;3、多个文件上传总大小：spring.servlet.multipart.max-request-size=大小；
&#8195;&#8195;2与3需要配置在application.properties或application.yml配置文件当中；
&#8195;4、代码模板（在controller中配置）：

```java
@PostMapping("/表单请求路径")
public String 函数名(文件上传相关参数){
    if(!headerImg.isEmpty()){
        String originalFilename=headerImg.getOriginalFilename();
        headerImg.transferTo(new File("文件保存路径"));
    }
    if(photos.length>0){
        for(MultipartFile photo:photos){
            if(!photo.isEmpty(){
                String originalFilename=photo.getOriginalFilename();
                photo.transferTo(new File("文件保存路径"));
            }
        }
    }
}
```

&#8195;&#8195;代码注意：
&#8195;&#8195;&#8195;headerImg为获取到的单个文件参数；
&#8195;&#8195;&#8195;photos为获取到的多个文件参数；



## 十三、单元测试Junit5

1、Junit5简介

Junit5包括Junit platform+Junit Jupriter+Junit Vintage；

SpringBoot2.4以上版本不支持Junit4(Junit Vintage)，要想支持Junit4，需要手动注入相关依赖；

SpringBoot整合了Junit后，编写测试方法使用Junit5版本的@Test注解，另外Junit类也具有Spring功能，例如是@Transactional注解：测试方法完成后自动回滚；

2、Junit5常用注释

（1）@Test：测试方法需要标注的注解；

（2）@DisplayName("xxx")：为测试方法添加展示名字，xxx为测试名字；

（3）@BeforeEach：在每个测试方法运行前运行；

（4）@AfterEach：在每个测试方法运行结束后运行；

（5）@BeforeAll：在所有测试方法开始前运行；

（6）@AfterAll：在所有测试方法结束后运行；

（7）@Tag：为某个测试方法打标签；

（8）@Disabled：代表当前测试方法被禁用；

（9）@Timeout：规定测试方法的运行时间，超过规定的运行时间则会抛出异常；

（10）@ExtendWith：为测试类或测试方法提供扩展类引用；

（11）@RepeatedTest(count)：重复执行当前的测试方法，count为重复执行的次数；

3、断言机制（assertions）

检查业务逻辑返回的数据是否合理；在所有测试方法运行结束后，会有一个详细的测试报告；

在使用断言机制前应导入包**org.junit.jupiter.api.Assertions**

断言常见类型：

（1）简单断言：用于对单个值进行验证；

常用验证函数方法：

| 方法            | 作用                                 |
| --------------- | ------------------------------------ |
| assertEquals    | 判断两个对象或两个原始类型是否相等   |
| assertNotEquals | 判断两个对象或两个原始类型是否不相等 |
| assertSame      | 判断两个对象引用是否指向同一个对象   |
| assertNotSame   | 判断两个对象引用是否指向不同的对象   |
| assertTrue      | 判断给定的布尔值是否为 true          |
| assertFalse     | 判断给定的布尔值是否为 false         |
| assertNull      | 判断给定的对象引用是否为 null        |
| assertNotNull   | 判断给定的对象引用是否不为 null      |

（2）数组断言：通过assertArrayEquals方法判断两个对象或原始类型的数组是否相等；

（3）组合断言：assertAll方法接受多个org.junit.jupiter.api.Executable函数式接口的实例作为要验证的断言，可以通过lambda表达式提供这些断言；

（4）异常断言：可以测试方法的异常情况，进而用于断言；

（5）超时断言：Assertions.assertTimeout方法为测试方法设置了超时时间，进而用于断言；

（6）快速失败：通过fail方法直接使得测试失败；

注意：在前面的断言方法失败后，后面的代码都不会执行

4、前置条件（assumptions）

不满足前置条件的测试方法将会提前终止执行；在使用时要导入assumptions的包；

5、嵌套测试

简单而言就是一个测试类里还含有一个测试类，而这个内嵌的测试类通常用@Nested注释标注；

注意：嵌套外层Test不能驱动内层的方法提前或者之后执行；但内层Test能够驱动外层的方法执行；

6、参数化测试

使用不同参数多数运行测试方法；在使用参数化测试时，要带有@ParameterizedTest注释进行标注；

常见的参数化测试类型标注：

（1）@ValueSource：为参数化测试指定参数来源，支持八大基础类以及String类型,Class类型；

（2）@NullSource：表示为参数化测试提供一个null的参数；

（3）@EnumSource：表示为参数化测试提供一个枚举参数；

（4）@CsvFileSource：表示读取指定CSV文件内容作为参数化测试的参数；

（5）@MethodSource：表示读取指定方法的返回值作为参数化测试的参数(注意方法返回需要是一个流)，使用时要指定方法名：@MethodSource("方法名")；



## 十四、SpringBoot Actuator

SpringBoot简化指标监控，抽取出Actuator场景，使得每个微服务快速引用即可获得生产级别的应用监控、审计等功能。

1、使用步骤：

（1）引入相关依赖场景；

（2）访问 http://localhost:8080/actuator/xx（xx为监控端点名称）；

（3）暴露所有监控信息为HTTP（http默认只暴露health和info端点），语法：

```java
management:
  endpoints:
    enabled-by-default: true //暴露所有端点信息
    web:
      exposure:
        include: '*'  //以web方式暴露
```

2、常用监控端点（Actuator Endpoint）

|                  |                                                              |
| ---------------- | ------------------------------------------------------------ |
| auditevents      | 暴露当前应用程序的审核事件信息。需要一个AuditEventRepository组件 |
| beans            | 显示应用程序中所有Spring Bean的完整列表                      |
| caches           | 暴露可用的缓存                                               |
| conditions       | 显示自动配置的所有条件信息，包括匹配或不匹配的原因           |
| configprops      | 显示所有@ConfigurationProperties                             |
| env              | 暴露Spring的属性ConfigurableEnvironment                      |
| flyway           | 显示已应用的所有Flyway数据库迁移。需要一个或多个Flyway组件   |
| health           | 显示应用程序运行状况信息                                     |
| httptrace        | 显示HTTP跟踪信息（默认情况下，最近100个HTTP请求-响应）。需要一个HttpTraceRepository组件 |
| info             | 显示应用程序信息                                             |
| integrationgraph | 显示Spring integrationgraph 。需要依赖spring-integration-core |
| loggers          | 显示和修改应用程序中日志的配置                               |
| liquibase        | 显示已应用的所有Liquibase数据库迁移。需要一个或多个`Liquibase`组件 |
| metrics          | 显示当前应用程序的“指标”信息                                 |
| mappings         | 显示所有@RequestMapping路径列表                              |
| scheduledtasks   | 显示应用程序中的计划任务                                     |
| sessions         | 允许从Spring Session支持的会话存储中检索和删除用户会话。需要使用Spring Session的基于Servlet的Web应用程序 |
| shutdown         | 使应用程序正常关闭。默认禁用                                 |
| startup          | 显示由ApplicationStartup收集的启动步骤数据。需要使用SpringApplication进行配置BufferingApplicationStartup |
| threaddump       | 执行线程转储                                                 |

最常用的监控端点：

（1）Health：健康检查端点，定时的检查应用的健康状况；

（2）Metrics：运行时指标；提供详细的、层级的、空间指标信息，这些信息可以被pull（主动推送）或者push（被动获取）方式得到；

（3）Loggers：日志记录；

3、端点管理

默认所有端点都是开启的；若需要手动指定某些端点的开启或禁用，要在application配置文件中配置，可以使用以下配置语法：

```java
management:
  endpoints:
    enabled-by-default: false   ///手动关闭所有的端点
  endpoint:
    beans:
      enabled: true     //手动开启beans端点
    health:
      enabled: true     //手动开启health端点
```

4、定制端点信息

（1）定制health端点信息

```java
//主要是重写AbstractHealthIndicator类下的doHealthCheck方法
@Component
public class xxxHealthIndicator extends AbstractHealthIndicator {
    /**
     * 类名必须是以HealthIndicator结尾
     */
    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        // 检查逻辑代码
        	// 可以使用builder.status设置状态
        	// 可以使用builder.withDetail("key", "value").withDetails(k);
    }
}
```

（2）定制info端点信息

1）配置application.yml文件实现

```java
info:
  appName: ""
  version: ""
  xxx: @yyy@   /使用@@可以获取值
  //例如：
  //mavenProjectName: @project.artifactId@  
  //mavenProjectVersion: @project.version@
```

2）编写InfoContributor接口的contribute方法

```java
@Component
public class xxxInfoContributor implements InfoContributor {
	/**
     * 类名必须是以InfoContributor结尾
     */
    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("example",
                Collections.singletonMap("key", "value"));
    }

}
```

（3）定制metrics端点信息

这是网上的一个例子：

```java
//这是用于监控函数被调用的次数的
public class MyService implements myservice{
    Counter counter;
    public MyService(MeterRegistry meterRegistry){
         counter = meterRegistry.counter("myservice.hello.count");  //指定被监控的方法
    }
    //被监控的方法
    public void hello() {
        //每被调用一次，会自动执行increment方法，counter就会+1
        counter.increment(); 
    }
}
```

定制的关键就是要引入MeterRegistry包并使用这个包的方法

5、自定义端点

```java
@Component
@Endpoint(id = "端点名")
public class 类名 {
    
    //端点的读操作
    @ReadOperation 
    public Map 函数名(){
        //逻辑代码
    }
    
    //端点的写操作
    @WriteOperation
    private void 函数名(){
        //逻辑代码
    }
}
```

SpringBoot可视化监控页面：https://github.com/codecentric/spring-boot-admin

