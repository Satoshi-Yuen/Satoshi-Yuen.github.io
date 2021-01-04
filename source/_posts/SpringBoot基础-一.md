---
title: SpringBoot基础(一)
date: 2021-01-03 22:18:07
tags:
- SpringBoot
---
SpringBoot：整合Spring技术栈的一站式框架，简化Spring技术栈的快速开发脚手架

一、初始化
创建maven项目，配置pom文件和注入依赖（官方文档）；
在主类上添加注释@SpringBootApplication：告知这是一个SpringBoot应用；
@RestController=@Controller+@ResponseBody：注释放在Controller类中；
二、依赖管理
父项目依赖管理：几乎声明所有开发中要用的依赖的版本号；
场景启动器：引入starter这个场景的所有常规都会自动引入；
以上均在pom文件中配合，官方文档有源码

二、自动配置
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

三、底层注解
1、@Configuration(proxyBeanMethods=true/false)：告诉SpringBoot是一个配置类==配置文件；
&#8195;（1）给容器中添加组件，以方法名作为组件id，返回类型是组件类型，返回的值是组件在容器中实例
&#8195;&#8195;*外部无论对配置类中的这个组件注册方法调用多少次获取的都是之前注册容器中的实例对象；
&#8195;&#8195;*配置类里面使用@Bean注释标注在方法上给容器注册组件，默认是单实例，配置类本身也是组件；
&#8195;（2）proxyBeanMethods：代理bean方法，参数选择：；
&#8195;&#8195;true：类组件之间有依赖关系方法调用得到之前单实例组件；
&#8195;&#8195;false：类组件之间无依赖关系；
2、@Import(...,...)：导入组件，给容器中自动创建出两个类型的组件，默认组件名是全类名；
3、@Conditional：条件装配，满足Conditional指定的条件则进行组件注入；
4、@ImportResource()：导入Spring配置文件，classpath:.....xml；
5、@ConfigurationProperties：配置绑定，只有在容器中的组件，才会有SpringBoot提供的功能；
6、@ConfigurationProperties+@Component：Dao类上配合；
7、@EnableConfigurationProperties(....class)：在主类上配置，参数为Dao类名.class；

四、自动配置原理
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

五、Spring最佳实践
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

六、yaml
yaml，标记语言，相当于properties，基本语法：
（1）key: value（键值对，冒号后有一空格）；
（2）区分大小写；
（3）使用缩进表示层级关系；要点：
&#8195;缩进只允许空格，不能使用tab，缩进空格数不限，只要相同层级的元素左对齐即可；
（4）"#"表示注释；
（5）双引号不会转义（有"\"相当于转义，转义再转义相当于不转义），单引号会转义（有"\"，相当于没变化，也就是已转义）；

七、静态资源规则与定制化
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

