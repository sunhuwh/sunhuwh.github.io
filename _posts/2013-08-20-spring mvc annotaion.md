---
layout: post
title: spring mvc annotaion
date: 2013-08-20 09:04
categories: [spring mvc]
tags: []
---

```plain
20130819 10:46:50,600  INFO [org.springframework.web.context.ContextLoader] Root WebApplicationContext: initialization started
20130819 10:46:50,711  INFO [org.springframework.web.context.support.XmlWebApplicationContext] Refreshing Root WebApplicationContext: startup date [Mon Aug 19 10:46:50 CST 2013]; root of context hierarchy
20130819 10:46:50,810  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp2\wtpwebapps\springmvc\WEB-INF\classes\applicationContext.xml]
20130819 10:46:50,933  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp2\wtpwebapps\springmvc\WEB-INF\classes\databaseContext.xml]
20130819 10:46:50,959  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp2\wtpwebapps\springmvc\WEB-INF\classes\servletContext.xml]
20130819 10:46:51,214  INFO [org.springframework.context.support.PropertySourcesPlaceholderConfigurer] Loading properties file from class path resource [database.properties]
20130819 10:46:51,279  INFO [org.springframework.beans.factory.support.DefaultListableBeanFactory] Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@1031310: defining beans [org.springframework.context.annotation.internalConfigurationAnnotationProcessor,org.springframework.context.annotation.internalAutowiredAnnotationProcessor,org.springframework.context.annotation.internalRequiredAnnotationProcessor,org.springframework.context.annotation.internalCommonAnnotationProcessor,org.springframework.context.annotation.internalPersistenceAnnotationProcessor,gson,org.springframework.context.support.PropertySourcesPlaceholderConfigurer#0,abcController,indexController,org.springframework.web.servlet.resource.ResourceHttpRequestHandler#0,org.springframework.web.servlet.handler.SimpleUrlHandlerMapping#0,org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping,org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter,org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter,localeResolver,messageSource,org.springframework.web.servlet.view.InternalResourceViewResolver#0,org.springframework.context.annotation.ConfigurationClassPostProcessor$ImportAwareBeanPostProcessor#0]; root of factory hierarchy
20130819 10:46:51,371  INFO [org.springframework.web.servlet.handler.SimpleUrlHandlerMapping] Mapped URL path [/resources2/**] onto handler 'org.springframework.web.servlet.resource.ResourceHttpRequestHandler#0'
20130819 10:46:51,417  INFO [org.springframework.web.context.ContextLoader] Root WebApplicationContext: initialization completed in 817 ms
这个是在没有加入<mvc:annotation-driven />所运行的结果，虽然没有报错，但是还是有问题，当我们访问的时候，根本就不能够用上spring mvc的annotation。
加上后的结果是：
20130819 10:49:04,642  INFO [org.springframework.web.context.ContextLoader] Root WebApplicationContext: initialization started
20130819 10:49:04,755  INFO [org.springframework.web.context.support.XmlWebApplicationContext] Refreshing Root WebApplicationContext: startup date [Mon Aug 19 10:49:04 CST 2013]; root of context hierarchy
20130819 10:49:04,863  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp2\wtpwebapps\springmvc\WEB-INF\classes\applicationContext.xml]
20130819 10:49:04,992  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp2\wtpwebapps\springmvc\WEB-INF\classes\databaseContext.xml]
20130819 10:49:05,021  INFO [org.springframework.beans.factory.xml.XmlBeanDefinitionReader] Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp2\wtpwebapps\springmvc\WEB-INF\classes\servletContext.xml]
20130819 10:49:05,339  INFO [org.springframework.context.support.PropertySourcesPlaceholderConfigurer] Loading properties file from class path resource [database.properties]
20130819 10:49:05,411  INFO [org.springframework.beans.factory.support.DefaultListableBeanFactory] Pre-instantiating singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@1669521: defining beans [org.springframework.context.annotation.internalConfigurationAnnotationProcessor,org.springframework.context.annotation.internalAutowiredAnnotationProcessor,org.springframework.context.annotation.internalRequiredAnnotationProcessor,org.springframework.context.annotation.internalCommonAnnotationProcessor,org.springframework.context.annotation.internalPersistenceAnnotationProcessor,gson,org.springframework.context.support.PropertySourcesPlaceholderConfigurer#0,abcController,indexController,org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping#0,org.springframework.format.support.FormattingConversionServiceFactoryBean#0,org.springframework.validation.beanvalidation.LocalValidatorFactoryBean#0,org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter#0,org.springframework.web.servlet.handler.MappedInterceptor#0,org.springframework.web.servlet.mvc.method.annotation.ExceptionHandlerExceptionResolver#0,org.springframework.web.servlet.mvc.annotation.ResponseStatusExceptionResolver#0,org.springframework.web.servlet.mvc.support.DefaultHandlerExceptionResolver#0,org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping,org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter,org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter,org.springframework.web.servlet.resource.ResourceHttpRequestHandler#0,org.springframework.web.servlet.handler.SimpleUrlHandlerMapping#0,localeResolver,messageSource,org.springframework.web.servlet.view.InternalResourceViewResolver#0,org.springframework.context.annotation.ConfigurationClassPostProcessor$ImportAwareBeanPostProcessor#0]; root of factory hierarchy
20130819 10:49:05,553  INFO [org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping] Mapped "{[/abc/get],methods=[POST],params=[],headers=[],consumes=[],produces=[],custom=[]}" onto public java.lang.String org.abc.controller.AbcController.get()
20130819 10:49:05,554  INFO [org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping] Mapped "{[/abc/index],methods=[GET],params=[],headers=[],consumes=[],produces=[],custom=[]}" onto public java.lang.String org.abc.controller.AbcController.index()
20130819 10:49:05,555  INFO [org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping] Mapped "{[/index],methods=[GET],params=[],headers=[],consumes=[],produces=[],custom=[]}" onto public java.lang.String org.abc.controller.IndexController.index()
20130819 10:49:05,581  INFO [org.hibernate.validator.util.Version] Hibernate Validator 4.1.0.Final
20130819 10:49:05,591  INFO [org.hibernate.validator.engine.resolver.DefaultTraversableResolver] Instantiated an instance of org.hibernate.validator.engine.resolver.JPATraversableResolver.
20130819 10:49:06,109  INFO [org.springframework.web.servlet.handler.SimpleUrlHandlerMapping] Mapped URL path [/resources2/**] onto handler 'org.springframework.web.servlet.resource.ResourceHttpRequestHandler#0'
20130819 10:49:06,136  INFO [org.springframework.web.context.ContextLoader] Root WebApplicationContext: initialization completed in 1493 ms
20130819 10:49:06,192  INFO [org.springframework.web.servlet.DispatcherServlet] FrameworkServlet 'root': initialization started
```

