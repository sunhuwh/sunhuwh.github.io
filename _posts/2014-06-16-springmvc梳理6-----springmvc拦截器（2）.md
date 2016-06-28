---
layout: post
title: springmvc梳理6-----springmvc拦截器（2）
date: 2014-06-16 02:26
categories: [spring mvc, E-learning, Spring]
tags: []
---

```java
public class HandlerInterceptor1 extends HandlerInterceptorAdapter {//此处一般继承HandlerInterceptorAdapter适配器即可
	/**
	 * 在preHandle中，可以进行编码、安全控制等处理； 
	 * 在postHandle中，有机会修改ModelAndView； 
	 * 在afterCompletion中，可以根据ex是否为null判断是否发生了异常，进行日志记录。
	*/
	
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("===========HandlerInterceptor1 preHandle");
        return true;
    }
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
    	/**
    	 * 修改了modelview，跳转到login这个页面中去了
    	 */
    	modelAndView.setViewName("/login");
        System.out.println("===========HandlerInterceptor1 postHandle");
    }
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
    	
        System.out.println("===========HandlerInterceptor1 afterCompletion");
    }
}
```
配置文件：

```html
	<!--
		<mvc:interceptors>:
		这个标签用于注册一个自定义拦截器或者是WebRequestInterceptors
		
		mvc:mapping:
		可以通过定义URL来进行路径请求拦截，可以做到较为细粒度的拦截控制。拦截特有的URL请求
		
		如果没有：<mvc:mapping path="/interceptorTest/**" />
		则表示拦截所有URL请求
		
	
	-->
	<mvc:interceptors>
	     <mvc:interceptor>
	            <mvc:mapping path="/interceptorTest/**" />
	            <bean class="com.boventech.learning.intercepter.HandlerInterceptor1" />
	     </mvc:interceptor>
    </mvc:interceptors>
```


