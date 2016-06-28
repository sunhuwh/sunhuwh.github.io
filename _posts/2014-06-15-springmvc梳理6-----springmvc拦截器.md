---
layout: post
title: springmvc梳理6-----springmvc拦截器
date: 2014-06-15 05:03
categories: [spring mvc, E-learning]
tags: []
---
在处理器之前或者之后进行处理某件事情：
1.日志记录：记录请求信息的日志，以便进行信息监控，信息统计等。
2.权限检查：如登录检测。进入处理器检测检测是否登录，如果没有返回到登陆页面去。
3.性能监控：有时候系统在某段时间莫名其妙的慢，可以通过拦截器在进入处理器之前记录开始时间，在处理完后记录结束时间，从而得到该请求的处理时间（如果有反向代理，如apache可以自动记录）；
4、通用行为：读取cookie得到用户信息并将用户对象放入请求，从而方便后续流程使用，还有如提取Locale、Theme信息等，只要是多个处理器都需要的即可使用拦截器实现。
5、OpenSessionInView：如Hibernate，在进入处理器打开Session，在完成后关闭Session。对于这个：
同样可以用filter来做：


```java
@WebFilter(filterName="openEntityManagerInViewFilter",urlPatterns={"/*"},asyncSupported=true)
public class OpenEntityManagerInViewFilter extends org.springframework.orm.jpa.support.OpenEntityManagerInViewFilter {

}
```

区别：

Filter主要是针对URL地址做一个编码的事情、过滤掉没用的参数、安全校验（比较泛的，比如登录不登录之类），太细的话，还是建议用interceptor
interceptor就比较多了，除了上述功能，还能监控调试方法性能问题，在页面加载时，通过postHandle方法置入一些页面上的公用参数值等。

拦截器的接口：


```java
package org.springframework.web.servlet;
public interface HandlerInterceptor {
	boolean preHandle(
			HttpServletRequest request, HttpServletResponse response, 
			Object handler) 
			throws Exception;

	void postHandle(
			HttpServletRequest request, HttpServletResponse response, 
			Object handler, ModelAndView modelAndView) 
			throws Exception;

	void afterCompletion(
			HttpServletRequest request, HttpServletResponse response, 
			Object handler, Exception ex)
			throws Exception;
} 
```

有三个方法，preHandle,postHandle,afterCompletion。
preHandle是在处理器之前就要执行的。一般是检查是否登录。
spring有一个实现HandlerInterceptor的类HandlerInterceptorAdapter：


```java
public abstract class HandlerInterceptorAdapter implements HandlerInterceptor {

	/**
	 * This implementation always returns <code>true</code>.
	 */
	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
	    throws Exception {
		return true;
	}

	/**
	 * This implementation is empty.
	 */
	public void postHandle(
			HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView)
			throws Exception {
	}

	/**
	 * This implementation is empty.
	 */
	public void afterCompletion(
			HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
			throws Exception {
	}

}
```

`有时候我们可能只需要实现三个回调方法中的某一个，如果实现`HandlerInterceptor接口的话，不管需不需要，三个方法必须实现，此时spring提供了一个HandlerInterceptorAdapter适配器（一种适配器设计模式的实现），允许只实现需要的回调方法。
preHandle：预处理回调方法，实现处理器的预处理（如登录检查），第三个参数为响应的处理器（如我们上一章的
Controller实现）；
返回值：true表示继续流程（如调用下一个拦截器或处理器）；
false表示流程中断（如登录检查失败），不会继续调用其他的拦截器或处理器，此时我们需要通过response来
产生响应；
postHandle：后处理回调方法，实现处理器的后处理（但在渲染视图之前），此时我们可以通过modelAndView（模
型和视图对象）对模型数据进行处理或对视图进行处理，modelAndView也可能为null。
afterCompletion：整个请求处理完毕回调方法，即在视图渲染完毕时回调，如性能监控中我们可以在此记录结束时间
并输出消耗时间，还可以进行一些资源清理，类似于try-catch-finally中的finally，但仅调用处理器执行链中
preHandle返回true的拦截器的afterCompletion。



