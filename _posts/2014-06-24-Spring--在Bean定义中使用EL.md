---
layout: post
title: Spring--在Bean定义中使用EL
date: 2014-06-24 00:33
categories: [E-learning, Spring]
tags: []
---

```java
/**
	 * 这个是xml风格注解
	 */
	@Test
	public void beanXml(){
		ApplicationContext ctx = new ClassPathXmlApplicationContext("/beanXml.xml");
		String world = ctx.getBean("world",String.class);
		String hello1 = ctx.getBean("hello1",String.class);
		String hello2 = ctx.getBean("hello2",String.class);
		String hello3 = ctx.getBean("hello3",String.class);
		System.out.println("world:"+world+";");
		System.out.println("hello1:"+hello1+";");
		System.out.println("hello2:"+hello2+";");
		System.out.println("hello3:"+hello3+";");
		Assert.assertEquals("Hello World1!", hello1);
	    Assert.assertEquals("Hello World!", hello2);
	    Assert.assertEquals("Hello World!", hello3);
	}
```



```html
<!-- SpEL支持在Bean定义时注入，默认使用“#{SpEL表达式}”表示 -->
	<!-- 模板默认以前缀“#{”开头，以后缀“}”结尾
	，且不允许嵌套
	，如“#{'Hello'#{world}}”错误，如“#{'Hello' + world}”中“world”默认解析为Bean。 -->
	<bean id="world" class="java.lang.String">
	   <constructor-arg value="#{' World!'}"/>
	</bean>
	<bean id="hello1" class="java.lang.String">
	    <constructor-arg value="#{'Hello'}#{world}"/>
	</bean>  
	<bean id="hello2" class="java.lang.String">
	    <constructor-arg value="#{'Hello' + world}"/>
	    <!-- 不支持嵌套的 -->
	    <!--<constructor-arg value="#{'Hello'#{world}}"/>-->
	</bean>
	<bean id="hello3" class="java.lang.String">
	    <constructor-arg value="#{'Hello' + @world}"/>
	</bean>
```

注解来做：


```java
public class SpELBean {
    
	/*
	 * 基于注解风格的SpEL配置
	 * 使用@Value注解来指定SpEL表达式
	 */
	@Value("#{'Hello' + world}")
	private String value;

	public String getValue() {
		return value;
	}

	public void setValue(String value) {
		this.value = value;
	}
}
```




```java
/**
	 * “helloBean1 ”值是SpEL表达式的值
	 * ，而“helloBean2”是通过setter注入的值，这说明setter注入将覆盖@Value的值。
	 * 
	 */
	@Test
	public void testAnnotationExpression() {
	    ApplicationContext ctx = new ClassPathXmlApplicationContext("/beanXml2.xml");
	    SpELBean helloBean1 = ctx.getBean("helloBean1", SpELBean.class);
	    Assert.assertEquals("Hello World!", helloBean1.getValue());
	    SpELBean helloBean2 = ctx.getBean("helloBean2", SpELBean.class);
	    Assert.assertEquals("haha", helloBean2.getValue());
	    
	    System.out.println(helloBean1.getValue());
	    System.out.println(helloBean2.getValue());
	}
	
```




```html
<!-- 配置时必须使用“<context:annotation-config/>”来开启对注解的支持。 -->
	<context:annotation-config/>
	<bean id="world" class="java.lang.String">
	    <constructor-arg value="#{' World!'}"/>
	</bean>
	<bean id="helloBean1" class="com.boventech.learning.bean.SpELBean"/>
	<bean id="helloBean2" class="com.boventech.learning.bean.SpELBean">
	    <property name="value" value="haha"/>
	</bean>
```



