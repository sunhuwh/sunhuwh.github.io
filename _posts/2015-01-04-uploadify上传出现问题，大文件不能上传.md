---
layout: post
title: uploadify上传出现问题，大文件不能上传
date: 2015-01-04 23:59
categories: [java]
tags: []
---
uploadify上传大文件404出问题ReferenceError: onQueueComplete is not defined
出现这种问题的原因是，


```html
<bean id="multipartResolver"
		class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
		<property name="maxUploadSize" value="10000000" />
	</bean>
```

设置的文件上传最大限制值小了，就会报错。

