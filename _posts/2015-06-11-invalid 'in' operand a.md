---
layout: post
title: invalid 'in' operand a
date: 2015-06-11 01:31
categories: [json]
tags: [json]
---
in对字符串不管用，需要对data进行处理


```java
$.get(url,function(data){
			obj= $.parseJSON(data); 
			$.each(obj, function(k,v) {
				alert(v.id);
            });
		});
```

