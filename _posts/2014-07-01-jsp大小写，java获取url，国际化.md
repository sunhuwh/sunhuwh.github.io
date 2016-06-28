---
layout: post
title: jsp大小写，java获取url，国际化
date: 2014-07-01 01:51
categories: [E-learning, Jsp, java]
tags: []
---

```java
@Controller
@RequestMapping("/toLowerCase")
public class ToLowerCaseController {
	/**
	 * JAVA 获取完整URL 方法
	 * @param request
	 * @return
	 */
	@RequestMapping(method=RequestMethod.GET)
	public String toLowerCase(HttpServletRequest request){
		System.out.println("ContextPath:"+request.getContextPath());
		System.out.println("ServletPath:"+request.getServletPath());
		return "toLowerCase/index";
	}

}

```



```html
<%@ page language="java" contentType="text/html; charset=utf-8"
    pageEncoding="utf-8"%>
    <%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions" %>
    <%@ taglib prefix="fmt" uri="http://java.sun.com/jstl/fmt_rt"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">

<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">
<title>Insert title here</title>
</head>
<body>
	ABC:${fn:toLowerCase("ABC") }<br/>
	abc:${fn:toUpperCase("abc") }<br/>
	ABCMESSAGE:<fmt:message key="ABC"/>
</body>
</html>
```

