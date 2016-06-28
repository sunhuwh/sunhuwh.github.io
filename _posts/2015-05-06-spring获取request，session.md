---
layout: post
title: spring获取request，session
date: 2015-05-06 00:35
categories: [java]
tags: []
---
web.xml中加：

	
	```html
	<listener>    
	        <listener-class>    
	            org.springframework.web.context.request.RequestContextListener
	        </listener-class>    
	</listener>
	```
	
	如果web.xml中有：
	
	```html
	<listener>
			<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
		</listener>
	```
	
	则没必要加。
	用这来获取：
	
	```java
	HttpServletRequest request = ((ServletRequestAttributes)RequestContextHolder.getRequestAttributes()).getRequest();
	```
	
	
	


