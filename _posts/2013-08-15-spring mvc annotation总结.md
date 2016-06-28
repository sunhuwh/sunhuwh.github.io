---
layout: post
title: spring mvc annotation总结
date: 2013-08-15 23:55
categories: [spring mvc]
tags: []
---
<context:annotation-config/>
他的作用是式地向 Spring 容器注册
AutowiredAnnotationBeanPostProcessor、CommonAnnotationBeanPostProcessor、PersistenceAnnotationBeanPostProcessor 以及 RequiredAnnotationBeanPostProcessor 这 4 个BeanPostProcessor。
注册这4个** **BeanPostProcessor的作用，就是为了你的系统能够识别相应的注解。

<context:component-scan base-package=”XX.XX”/> 
该配置项其实也包含了自动注入上述processor的功能。**
**

<mvc:argument-resolvers>
允许注册实现了WebArgumentResolver接口的bean，来对handlerMethod中的用户自定义的参数或annotation进行解析


```html
	<mvc:annotation-driven validator="validator">
		<mvc:argument-resolvers>
			<bean
				class="net.zhepu.web.handlers.argumentHandler.MyCustomerWebArgumentHandler" />
		</mvc:argument-resolvers>

	</mvc:annotation-driven>
```

对应的java


```java
public class MyCustomerWebArgumentHandler implements WebArgumentResolver {

	@Override
	public Object resolveArgument(MethodParameter methodParameter,
			NativeWebRequest webRequest) throws Exception {
		if (methodParameter.getParameterType().equals(MyArgument.class)) {
			MyArgument argu = new MyArgument();
			argu.setArgumentName("winzip");
			argu.setArgumentValue("123456");
			return argu;
		}
		return UNRESOLVED;
	}

}
```


@Controller、@Service 以及 @Repository 和 @Component 注解的作用是等价的：将一个类成为 Spring 容器的 Bean。
如果是没有用@Service之前，是用xml，写个bean。至于以前xml中需要注入Dao，现在则不需要了。
由于 Spring MVC 的 Controller 必须事先是一个 Bean，所以 @Controller 注解是不可缺少的。


```java
@RequestMapping(value = "/image",method = RequestMethod.GET)
    ModelAndView index(@RequestParam(value="page",required=false, defaultValue="1") int page)
```
@RequestParam注解可以用来提取名为“number”的String类型的参数，并将之作为输入参数传入。


```java
@RequestMapping(value = "/image/{id}", method = RequestMethod.GET)
    ModelAndView toEdit(@PathVariable long id)
```
{id}在这个请求的URL里就是个变量，可以使用@PathVariable来获取
@PathVariable和@RequestParam的区别就在于：@RequestParam用来获得静态的URL请求入参数

