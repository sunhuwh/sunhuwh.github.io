---
layout: post
title: Spring配置 <context:component-scan/> <mvc:annotation-driven />
date: 2014-05-11 23:36
categories: [spring mvc, servlet, E-learning, Spring]
tags: [contextcomponent-sca, mvcannotation-driven]
---
<annotaion-driven/>标签：
这个标签对应的实现类是org.springframework.web.servlet.config.AnnotationDrivenBeanDefinitionParser
仔细阅读它的注释文档可以很明显的看到这个类的作用。解析这个文档：
这个类主要注册8个类的实例：
1.RequestMappingHandlerMapping
2.BeanNameUrlHandlerMapping
3.RequestMappingHandlerAdapter
4.HttpRequestHandlerAdapter
5.SimpleControllerHandlerAdapter
6.ExceptionHandlerExceptionResolver
7.ResponseStatusExceptionResolver
8.DefaultHandlerExceptionResolver
1是处理@RequestMapping注解的，2.将controller类的名字映射为请求url。1和2都实现了HandlerMapping接口，用来处理请求映射。
3是处理@Controller注解的控制器类，4是处理继承HttpRequestHandlerAdapter类的控制器类，5.处理继承SimpleControllerHandlerAdapter类的控制器。所以这三个是用来处理请求的。具体点说就是确定调用哪个controller的哪个方法来处理当前请求。
6,7,8全部继承AbstractHandlerExceptionResolver，这个类实现HandlerExceptionResolver，该接口定义：接口实现的对象可以解决处理器映射、执行期间抛出的异常，还有错误的视图。
所以<annotaion-driven/>标签主要是用来帮助我们处理请求映射，决定是哪个controller的哪个方法来处理当前请求，异常处理。

<context:component-scan/>标签：
它的实现类是org.springframework.context.annotation.ComponentScanBeanDefinitionParser.
把鼠标放在context:component-scan上就可以知道有什么作用的，用来扫描该包内被@Repository @Service @Controller的注解类，然后注册到工厂中。并且context:component-scan激活@ required。@ resource,@ autowired、@PostConstruct @PreDestroy @PersistenceContext @PersistenceUnit。使得在适用该bean的时候用@Autowired就行了。



