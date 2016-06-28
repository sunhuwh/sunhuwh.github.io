---
layout: post
title: java通过监听Session实现统计在线用户
date: 2014-08-31 23:47
categories: [E-learning, 工具, java]
tags: []
---

```java
package com.boventech.learning.listener;

import java.util.HashSet;
import java.util.Set;

import javax.servlet.ServletContextAttributeEvent;
import javax.servlet.ServletContextAttributeListener;
import javax.servlet.http.HttpSessionAttributeListener;
import javax.servlet.http.HttpSessionBindingEvent;

import com.boventech.learning.constants.Constants;
import com.boventech.learning.entity.User;


public class SessionListener implements ServletContextAttributeListener, HttpSessionAttributeListener {

	private static Set<User> onLineUsers = new HashSet<User>();//用于保存在线用户

	public static Set<User> getOnLineUsers() {
		return onLineUsers;
	}

        //session创建后触发   ，将用户信息添加到静态的集合中
	public void attributeAdded(HttpSessionBindingEvent arg0) {
		if(arg0.getName().equals(Constants.USER_KEY)){
			onLineUsers.add((User)arg0.getValue());
		}
	}
        //清除session时触发
	public void attributeRemoved(HttpSessionBindingEvent arg0) {
		if(arg0.getName().equals(Constants.USER_KEY)){
			onLineUsers.remove((User)arg0.getValue());
		}
	}
        //session被替换时触发
	public void attributeReplaced(HttpSessionBindingEvent arg0) {
		if(arg0.getName().equals(Constants.USER_KEY)){
			onLineUsers.add((User)arg0.getValue());
		}
		
	}

	public void attributeAdded(ServletContextAttributeEvent arg0) {	

	}
	public void attributeRemoved(ServletContextAttributeEvent arg0) {

	}
	public void attributeReplaced(ServletContextAttributeEvent arg0) {

	}
}
```



```html
<listener>
	  <listener-class>com.boventech.learning.listener.SessionListener</listener-class>
	</listener>
```



