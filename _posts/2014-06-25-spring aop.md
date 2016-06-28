---
layout: post
title: spring aop
date: 2014-06-25 01:57
categories: [E-learning, Spring]
tags: []
---

```java
package com.boventech.learning.service;

/**
 * 定义目标接口
 * @author thinkpad
 *
 */
public interface IHelloWorldService {
    public void sayHello();
}
```



```java
package com.boventech.learning.serviceImpl;

import com.boventech.learning.service.IHelloWorldService;
/**
 * 定义目标接口实现
 * @author thinkpad
 *
 */
public class HelloWorldServiceImpl implements IHelloWorldService {
    @Override
    public void sayHello() {
        System.out.println("============Hello World!");
    }
}

```


```java
package com.boventech.learning.aspect;

/**
 * 此处HelloWorldAspect类不是真正的切面实现，只是定义了通知实现的类，在此我们可以把它看作就是缺少了切入点的切面。
 * @author thinkpad
 *
 */
public class HelloWorldAspect {
    //前置通知
	public void beforeAdvice() {
		 System.out.println("===========before advice");
	}
	//后置最终通知
	public void afterFinallyAdvice() {
		System.out.println("===========after finally advice");
	}
}
```


```html
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:mongo="http://www.springframework.org/schema/data/mongo"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xsi:schemaLocation="http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.1.xsd
		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.1.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.1.xsd 
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.1.xsd 
		http://www.springframework.org/schema/data/mongo http://www.springframework.org/schema/data/mongo/spring-mongo-1.0.xsd ">
	<!-- 配置切面 -->
	<!-- 切入点使用<aop:config>标签下的<aop:pointcut>配置，expression属性用于定义切入点模式，默认是AspectJ语法
	，“execution(* com.boventech..*.*(..))”表示匹配com.boventech包及子包下的任何方法执行。
	切面使用<aop:config>标签下的<aop:aspect>标签配置，其中“ref”用来引用切面支持类的方法。
	前置通知使用<aop:aspect>标签下的<aop:before>标签来定义，pointcut-ref属性用于引用切入点Bean
	，而method用来引用切面通知实现类中的方法，该方法就是通知实现，即在目标类方法执行之前调用的方法。
	最终通知使用<aop:aspect>标签下的<aop:after >标签来定义，切入点除了使用pointcut-ref属性来引用已经存在的切入点，也可以使用pointcut属性来定义
	，如pointcut="execution(* com.boventech..*.*(..))"，method属性同样是指定通知实现，即在目标类方法执行之后调用的方法。
	
	 -->
	<bean id="helloWorldService" class="com.boventech.learning.serviceImpl.HelloWorldServiceImpl"/>
	
	<bean id="aspect" class="com.boventech.learning.aspect.HelloWorldAspect"/>
	<aop:config>
	<aop:pointcut id="pointcut" expression="execution(* com.boventech..*.*(..))"/>
	    <aop:aspect ref="aspect">
	        <aop:before pointcut-ref="pointcut" method="beforeAdvice"/>
	        <aop:after pointcut="execution(* com.boventech..*.*(..))" method="afterFinallyAdvice"/>
	    </aop:aspect>
	</aop:config>
</beans>
```


```java
package com.boventech.learning.aspect;

import org.junit.Test;
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

import com.boventech.learning.service.IHelloWorldService;

public class AopTest {

	@Test
    public void testHelloworld() {
        ApplicationContext ctx =  new ClassPathXmlApplicationContext("/helloworld.xml");
        IHelloWorldService helloworldService =
        ctx.getBean("helloWorldService", IHelloWorldService.class);
        helloworldService.sayHello();
    }

}

```

