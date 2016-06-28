---
layout: post
title: spring AspectJ order(顺序)
date: 2014-06-29 00:31
categories: [E-learning, Spring]
tags: []
---

```java
@Aspect
@Order(2)
public class HelloWorldAspectAnnotation {
	/**
	 * JoinPoint接口
	 * @param joinPoint
	 */
	/*public interface JoinPoint {
	    String toString();         //连接点所在位置的相关信息
	    String toShortString();     //连接点所在位置的简短相关信息
	    String toLongString();     //连接点所在位置的全部相关信息
	    Object getThis();         //返回AOP代理对象
	    Object getTarget();       //返回目标对象
	    Object[] getArgs();       //返回被通知方法参数列表
	    Signature getSignature();  //返回当前连接点签名
	    SourceLocation getSourceLocation();//返回连接点方法所在类文件中的位置
	    String getKind();        //连接点类型
	    StaticPart getStaticPart(); //返回连接点静态部分
	}*/
	
	
    //定义前置通知，注意这里是sayHello2
	//使用@Before进行前置通知声明，其中value用于定义切入点表达式或引用命名切入点
	@Before(value="execution(* com.boventech..*.sayHello2(..))&& args(param)",argNames="param")
	public void beforeAdvice(JoinPoint joinPoint,String param) {
		System.out.println(1);
		System.out.println("=======================");
		System.out.println("===param:" + param);
		System.out.println("=======================");
		System.out.println(joinPoint.getArgs().length);
		System.out.println("=======================");
		System.out.println(joinPoint.toString());
		System.out.println("=======================");
		System.out.println(joinPoint.getTarget());
		System.out.println("=======================");
		System.out.println(joinPoint.getThis());
		System.out.println("=======================");
		System.out.println("===========before advice");
	}
	/*value：指定切入点表达式或命名切入点；
    pointcut：同样是指定切入点表达式或命名切入点，如果指定了将覆盖value属性指定的，pointcut具有高优先级；*/
	@AfterReturning(value="execution(* com.boventech..*.sayHello2(..))&& args(param)",argNames="param",pointcut="execution(* com.boventech..*.sayHello2(..))&& args(param)")
	public void afterFinallyAdvice(JoinPoint joinPoint,String param) {
		System.out.println("param:"+param);
		System.out.println("===========");
		System.out.println("===========after finally advice");
	}
}

```




```java
@Aspect
@Order(1)
public class HelloWorldAspectAnnotation2 {
	/**
	 * JoinPoint接口
	 * @param joinPoint
	 */
	/*public interface JoinPoint {
	    String toString();         //连接点所在位置的相关信息
	    String toShortString();     //连接点所在位置的简短相关信息
	    String toLongString();     //连接点所在位置的全部相关信息
	    Object getThis();         //返回AOP代理对象
	    Object getTarget();       //返回目标对象
	    Object[] getArgs();       //返回被通知方法参数列表
	    Signature getSignature();  //返回当前连接点签名
	    SourceLocation getSourceLocation();//返回连接点方法所在类文件中的位置
	    String getKind();        //连接点类型
	    StaticPart getStaticPart(); //返回连接点静态部分
	}*/
	
	
    //定义前置通知，注意这里是sayHello2
	//使用@Before进行前置通知声明，其中value用于定义切入点表达式或引用命名切入点
	@Before(value="execution(* com.boventech..*.sayHello2(..))&& args(param)",argNames="param")
	public void beforeAdvice(JoinPoint joinPoint,String param) {
		System.out.println(2);
		System.out.println("=======================");
		
	}
	
	/*value：指定切入点表达式或命名切入点；
    pointcut：同样是指定切入点表达式或命名切入点，如果指定了将覆盖value属性指定的，pointcut具有高优先级；*/
	@AfterReturning(value="execution(* com.boventech..*.sayHello2(..))&& args(param)",argNames="param",pointcut="execution(* com.boventech..*.sayHello2(..))&& args(param)")
	public void afterFinallyAdvice(JoinPoint joinPoint,String param) {
		System.out.println("order:" + 2);
	}
}
```


```java
public class AopAnnotationTest {
	
	@Test
    public void testHelloworld() {
        ApplicationContext ctx =  new ClassPathXmlApplicationContext("/helloWorld2.xml");
        IHelloWorld2Service helloworldService =ctx.getBean("helloWorld2Service", IHelloWorld2Service.class);
        String param = "12";
        helloworldService.sayHello2(param);
    }

}
```


```html
<aop:aspectj-autoproxy/>
	<bean id="helloWorld2Service" class="com.boventech.learning.serviceImpl.HelloWorld2ServiceImpl"/>
	
    <bean id="aspect"
             class="com.boventech.learning.aspect.HelloWorldAspectAnnotation"/>
             
    <bean id="aspect2"
             class="com.boventech.learning.aspect.HelloWorldAspectAnnotation2"/>
```

