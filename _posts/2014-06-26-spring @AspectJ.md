---
layout: post
title: spring @AspectJ
date: 2014-06-26 01:01
categories: [E-learning, Spring]
tags: [AspectJ]
---

```java
/**
 * 定义目标接口
 * @author thinkpad
 *
 */
public interface IHelloWorld2Service {
    public void sayHello2();
}
```



```java
/**
 * 定义目标接口实现
 * @author thinkpad
 *
 */
public class HelloWorld2ServiceImpl implements IHelloWorld2Service {
	//使用@Pointcut进行命名切入点声明
	@Pointcut(value="execution(* com.boventech..*.HelloWorld2ServiceImpl(..))")
    @Override
    public void sayHello2() {
        System.out.println("============Hello World!");
    }
}
```




```java
//使用@Aspect将POJO声明为切面；
@Aspect
public class HelloWorldAspectAnnotation {
    //定义前置通知，注意这里是sayHello2
	//使用@Before进行前置通知声明，其中value用于定义切入点表达式或引用命名切入点
	@Before(value="execution(* com.boventech..*.sayHello2(..))")
	public void beforeAdvice() {
		 System.out.println("===========before advice");
	}
	/*value：指定切入点表达式或命名切入点；
    pointcut：同样是指定切入点表达式或命名切入点，如果指定了将覆盖value属性指定的，pointcut具有高优先级；*/
	@AfterReturning(value="execution(* com.boventech..*.sayHello2(..))",pointcut="execution(* com.boventech..*.sayHello2(..))")
	public void afterFinallyAdvice() {
		System.out.println("===========after finally advice");
	}
}
```


helloWorld2.xml


```html
<!-- 配置文件需要使用<aop:aspectj-autoproxy/>来开启注解风格的@AspectJ支持 
	   需要将切面注册为Bean，如“aspect”Bean
	-->
	<aop:aspectj-autoproxy/>
	<bean id="helloWorld2Service" class="com.boventech.learning.serviceImpl.HelloWorld2ServiceImpl"/>
	
    <bean id="aspect"
             class="com.boventech.learning.aspect.HelloWorldAspectAnnotation"/>
```




```java
@Test
    public void testHelloworld() {
        ApplicationContext ctx =  new ClassPathXmlApplicationContext("/helloWorld2.xml");
        IHelloWorld2Service helloworldService =ctx.getBean("helloWorld2Service", IHelloWorld2Service.class);
        helloworldService.sayHello2();
    }
```



