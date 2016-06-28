---
layout: post
title: springmvc梳理3 DispatcherServlet
date: 2014-06-13 01:27
categories: [E-learning, spring mvc]
tags: []
---
contextLoadListener初始化上下文和DispatcherServlet初始化上下文的关系：
![](http://sishuok.com/forum/upload/2012/7/21/664811d1be029d66250bfe66d65fbe4f__1.JPG)
可以看到DispatcherServlet初始化的上下文是继承于ContextLoaderListener初始化的上下文的。所以，ContextLoaderListener初始化的上下文加载的Bean是对于整个应用程序共享的，不管是使用什么表现层技术，一般如DAO层、Service层Bean
而DispatcherServlet初始化的上下文所加载的bean只是在其内部共享的。DispatcherServlet初始化的bean都是关于web层的，DispatcherServlet是前端控制器设计模式的实现，提供Spring Web MVC的集中访问点，而且负责职责的分派：
DispatcherServlet主要用作职责调度工作，本身主要用于控制流程，主要职责如下：
1、文件上传解析，如果请求类型是multipart将通过MultipartResolver进行文件上传解析；
2、通过HandlerMapping，将请求映射到处理器（返回一个HandlerExecutionChain，它包括一个处理器、多个HandlerInterceptor拦截器）；
3、通过HandlerAdapter支持多种类型的处理器(HandlerExecutionChain中的处理器)；
4、通过ViewResolver解析逻辑视图名到具体视图实现；
5、本地化解析；
6、渲染具体的视图等；
7、如果执行过程中遇到异常将交给HandlerExceptionResolver来解析。
从以上我们可以看出DispatcherServlet主要负责流程的控制（而且在流程中的每个关键点都是很容易扩展
的）。
而ContextLoaderListener一般初始化的是DAO层、Service层Bean。
根据以上，配置文件也可以规范化起来。
例如context:component-scan，像Dao和Service层bean，用contextLoadListener的上下文加载就行了。虽然用DispatcherServlet也行，但是还是有些违背springmvc的规范。
这样也形成一种隔离，DispatcherServlet可以调用contextLoadListener上下文加载的bean，而DispatcherServlet不能调用ContextLoaderListener上下文加载的bean。

对于这些，在eclipse console里面都可以看见。比如：
[School InFormatization -->]--> INFO{ContextLoader.java:272}-Root WebApplicationContext: initialization started
  [School InFormatization -->]--> INFO{AbstractApplicationContext.java:500}-Refreshing Root WebApplicationContext: startup date [Thu Jun 12 16:59:10 CST 2014]; root of context hierarchy
  [School InFormatization -->]--> INFO{XmlBeanDefinitionReader.java:315}-Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp8\wtpwebapps\E-learning2\WEB-INF\classes\applicationContext.xml]
  [School InFormatization -->]--> INFO{XmlBeanDefinitionReader.java:315}-Loading XML bean definitions from file [D:\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp8\wtpwebapps\E-learning2\WEB-INF\classes\contextLoaderListenerContext.xml]
.
.
同样的代码，没有规范的和规范了的，启动时间上差别还是有点大的。没有规范的：信息: Server startup in 7759 ms，规范了的：信息: Server startup in 7413 ms，多了两秒。这是一个比较小的项目进行测试的，功能代码完全相同，就是把配置文件进行了修改。相差0.3秒。虽然看着不大，但是还是有性能上的差异的。
未规范：就是用dispatcherServlet完成本该ContextLoaderListener完成的事。




