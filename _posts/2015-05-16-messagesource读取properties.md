---
layout: post
title: messagesource读取properties
date: 2015-05-16 23:59
categories: [java]
tags: []
---
#xml中配置：


```html
<bean id="messageSource"
		class="org.springframework.context.support.ReloadableResourceBundleMessageSource">
		<property name="basenames">
			<array>
				<value>classpath:web</value>
			</array>
		</property>
	</bean>
```

程序中注入：

```java
@Resource
	private MessageSource messageSource;
```

获取：

```java
String username = messageSource.getMessage("username", new Object[]{}, LocaleContextHolder.getLocale());
```

