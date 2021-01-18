---
title: SpringSecurity登录方面的一二事
date: 2021-01-18 16:44:41
tags:
- SpringSecurity
---

以下是学习关于SpringSecurity在做登陆功能方面的笔记总结

## 前期工作

1、确保为thymeleaf引擎

2、引入SpringSecurity场景依赖模块

```java
<dependencies>
    <!-- ... other dependency elements ... -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
</dependencies>
```

3、编写SpringSecurity配置，由于配置都已经ok了，所以只要写一个配置类（配置类必须继承WebSecurityConfigurerAdapter）：

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    //逻辑代码
}
```



## 一、登录认证&授权&权限控制

以下代码参照官方文档：

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

	@Override
	protected void configure(HttpSecurity http) throws Exception {
        //定制请求的权限规则，没有登录会自动跳到默认的登陆页面
		http
			.authorizeRequests()
				.antMatchers("/css/**", "/index").permitAll()	//这些路径允许所有人访问	
				.antMatchers("/user/**").hasRole("USER")	    //定制访问身份（权限）		
				.and()
			.formLogin()  //开启自动配置登录功能，登录页是自动配置好的
				.loginPage("/login").failureUrl("/login-error");
	}

        
    //定制认证规则
	@Autowired
	public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
		auth
			.inMemoryAuthentication()        //这是在内存中查用户，实际上连接数据库
				.withUser("user").password("password").roles("USER");
	}
}
```



## 二、注销

1、在配置类中开启注销功能：http.logout()；

2、要点：

（1）注销成功后会返回到/login/logout（默认的登陆页面）；

（2）访问/logout表示用户注销并清空session；

（3）定制注销后的跳转页面：http.logout().logoutSuccessUrl("路径");



## 三、“记住我”功能&定制登陆页

1、“记住我”功能：登录成功后，将cookie发给浏览器保存，以后访问页面带上这个cookie，只要通过检查就可以免登录，要点：

（1）在配置类中开启“记住我”功能：http.rememberMe();若想要定制“记住我”功能，则：http.rememberMe().rememberMeParameter("控件name");

（2）点击注销会删除cookie，“记住我”功能消失；

2、登陆页定制

由于默认的登录为get请求，若使用自己定制的登陆页则默认是post请求，语法：http.formLogin().usernameParameter("表单用户名name").passwordParameter("表单密码name").loginPage("/login");

可以配合使用thymeleaf语法定制登录首页后显示的内容，例如：

```html
<!--sec:authorize：判定认证，验证登录权限，判断成功后可显示此权限对应的内容-->
<div th:fragment="logout" class="logout" sec:authorize="isAuthenticated()">		
    <!--sec:authentication：可获取登录信息-->
            Logged in user: <span sec:authentication="name"></span> |					
            Roles: <span sec:authentication="principal.authorities"></span>				
            <div>
                <form action="#" th:action="@{/logout}" method="post">					
                    <input type="submit" value="Logout" />
                </form>
            </div>
        </div>
```



