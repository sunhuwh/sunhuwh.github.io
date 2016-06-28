---
layout: post
title: 自建一个WebApplicationInitializer
date: 2014-05-11 00:15
categories: [E-learning, servlet, Spring]
tags: []
---
昨天的blog中提到，实现WebApplicationinitializer的类都可以在web应用程序启动时被加载。
这个是通过SpringServletContainerIntializer实现ServletContainerIntializer才能实现的。
我自己建了一个项目用来实现这种方式：
首先建个WebApplicationInitializer.java


```java
package com.boventech.config;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;


/**
 * WebApplicationInitializer接口
 * @author hu.sun
 */

public interface WebApplicationInitializer{
	
	public  void config(ServletContext context) throws ServletException;
	
}

```


继续，由于必须通过SpringServletContailnerIntializer才能加载，再建个SpringServletContailnerIntializer类：


```java
package com.boventech.config;

import java.lang.reflect.Modifier;
import java.util.Set;

import javax.servlet.ServletContainerInitializer;
import javax.servlet.ServletContext;
import javax.servlet.ServletException;
import javax.servlet.annotation.HandlesTypes;



@HandlesTypes(WebApplicationInitializer.class)  
public class SpringServletContainerInitializer implements ServletContainerInitializer{
	@Override
	public void onStartup(Set<Class<?>> webApplicationInitializers, ServletContext servletContext)
			throws ServletException {
		if (webApplicationInitializers != null) {
			for (Class<?> webApplicationInitializerClass : webApplicationInitializers) {
				if (!webApplicationInitializerClass.isInterface() && !Modifier.isAbstract(webApplicationInitializerClass.getModifiers()) &&
						WebApplicationInitializer.class.isAssignableFrom(webApplicationInitializerClass)) {
					try {
						((WebApplicationInitializer) webApplicationInitializerClass.newInstance()).config(servletContext);
					}
					catch (Throwable ex) {
						throw new ServletException("Failed to instantiate webApplicationInitializer class", ex);
					}
				}
			}
		}
	}
}

```

注意：要实现ServletContainerInitializer接口，必须指定实现的类。@HandlesTypes就起到关键性作用。
还有一个最重要的：就是昨天提到的，在Libraries->Spring -web-x.x.x.jar->META-INF/services/javax.servlet.ServletContainerInitializer里面的内容必须是实现ServletContainerInitializer的类。想要的是com.boventech.config.SpringServletContainerInitializer。所以建个jar包，结构和这个一样META-INF/services/javax.servlet.ServletContainerInitializer，内容变了，实现类的路径。
然后就可以运行了。



```java
package com.boventech.config;

import javax.servlet.ServletContext;
import javax.servlet.ServletException;

import org.springframework.web.context.ContextLoaderListener;
import org.springframework.web.util.WebAppRootListener;

public class DefaultServletConfig implements WebApplicationInitializer{

	@Override
	public void config(ServletContext servletContext)  throws ServletException{
		servletContext.addListener(new ContextLoaderListener());
		servletContext.addListener(new WebAppRootListener());
		servletContext.setInitParameter("contextConfigLocation", "classpath*:**/*Context.xml");
		//设置webAppRootKey得值以得到根目录
		servletContext.setInitParameter("webAppRootKey", "learning");
	}
}

```
通过建这样一个项目我明白了 servlet的contextLoadListener和WebAppRootListener的原理。
WebApplicationinitializer工作原理。



