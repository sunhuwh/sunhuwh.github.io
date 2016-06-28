---
layout: post
title: spring mvc
date: 2013-08-15 00:01
categories: [spring mvc]
tags: [spring mvc]
---
`spring是围绕着DispatcherServlet进行设计的。`
请求被处理程序处理，处理程序的默认接口是Controler接口。
``
`
`
`SimpleFormContoller`提供了显示从`HTTP GET`请求接收到的表单的功能，以及处理从`HTTP POST`接收到的相同表单数据的功能。

ModelAndView包含视图和数据。有了它，就可以通过它来定视图和传的数据。

spring mvc的工作原理：
先加载前端控制器，默认的DispacherServlet。
根据前端控制器的映射请求，再参照控制器配置文件，将请求交给后端控制器进行处理。
后端调用逻辑层代码处理并将视图对象和数据对象交给前端控制器。
前端控制器根据后端的视图对象来返回页面。

struts2的工作原理，
先加载前端控制器；
根据前端控制器的映射请求，参照控制器配置文件struts.xml，将请求交给后端控制器进行处理；
后端调用逻辑层处理，返回的是数据对象和返回值。
后端控制器根据返回值来决定返回页面。
然后交给前端来返回。

对比struts2，spring mvc他们的本质区别就在于，逻辑层可返回视图对象和数据对象。struts是分两步干的。


**<servlet-name>-mvc.xml 配置**:

```java
<!-- 自动扫描的包名 -->  
    <context:component-scan base-package="" ></context:component-scan> 
```


<context:component-scan/> 扫描指定的包中的类上的注解，常用的注解有：
@Controller 声明Action组件
@Service    声明Service组件    @Service("myMovieLister")
@Repository 声明Dao组件
@Component   泛指组件, 当不好归类时.
@RequestMapping("/menu")  请求映射
@Resource  用于注入，( j2ee提供的 ) 默认按名称装配，@Resource(name="beanName")
@Autowired 用于注入，(srping提供的) 默认按类型装配
@Transactional( rollbackFor={Exception.class}) 事务管理
@ResponseBody
@Scope("prototype")   设定bean的作用域
@Controller、@Service 以及 @Repository 和 @Component 注解的作用是等价的：将一个类成为 Spring 容器的 Bean。由于 Spring MVC 的 Controller 必须事先是一个 Bean，所以 @Controller 注解是不可缺少的。

前置控制器  DispatcherServlet  web.xml中
HandlerHandlerMapping接口，处理请求的映射
其实现类：
SimpleUrlHandlerMapping  通过配置文件把URL映射至Controller
DefaultAnnotationHandlerMapping  通过注解把URL映射到Controller
HandlerAdapter接口  同样是处理请求的映射
其实现类：
AnnotationMethodHandlerAdapter 通过注解把URL映射到Controller

Controller接口 --- 控制器
@Controller  添加了它的类就可担当控制器的责任
HandlerInterceptor接口 ---- 拦截器
DispatcherServlet初始化过程中，会在WEB-INF文件夹下找[Servlet-name]-servlet.xml，生成文件中定义的Bean。

<mvc:annotation-driven /> 会自动注册DefaultAnnotationHandlerMapping与AnnotationMethodHandlerAdapter 两个bean,是spring MVC为@Controllers分发请求所必须的。

如何访问静态文件，如css、js、jpg。
当DispatcherServlet拦截的是*.do,那么上面的问题不存在；
但是如果当拦截的是/，那么会拦截所有，包括上面的，如何解决上面的问题呢？
1.可通过mvc-resources来解决，如：


```java
    <!-- 对静态资源文件的访问 -->    
    <mvc:resources mapping="/images/**" location="/images/" />  
```
2.通过

```java
<mvc:default-servlet-handler/>
```



借鉴文章：http://elf8848.iteye.com/blog/875830
   