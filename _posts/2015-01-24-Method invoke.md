---
layout: post
title: Method invoke
date: 2015-01-24 00:21
categories: [java]
tags: []
---

```java
package duri;

import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class MethodTest {
	
	public static void getUserName() throws IllegalAccessException, IllegalArgumentException, InvocationTargetException{
		User user = new User();
		user.setUsername("admin");
		user.setPassword("123456");
		Method[] methods = User.class.getDeclaredMethods();
		for(Method method : methods){
			if("getUsername".equals(method.getName())){
				System.out.println(method.invoke(user));
			}
		}
	}
	
	public static void main(String[] args) throws IllegalAccessException, IllegalArgumentException, InvocationTargetException {
		getUserName();
	}

}

```



```java
package duri;

public class User {

public String username;

public String password;

public String getUsername() {
return username;
}

public void setUsername(String username) {
this.username = username;
}

public String getPassword() {
return password;
}

public void setPassword(String password) {
this.password = password;
}



}

```

