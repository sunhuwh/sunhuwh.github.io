---
layout: post
title: springmvc上传临时文件目录配置
date: 2015-09-09 22:04
categories: [spring mvc]
tags: [spring mvc]
---
	<beanid="multipartResolver"class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
	        <propertyname="uploadTempDir"value = "/upload"></property>
	        <!-- <property name="maxUploadSize" value="10000000" /> -->
	    </bean>
uploadTempDir属性。
但是这个属性只能帮助我们将上传目录指向tomcat。
而如果想指向外面，可以利用windows建立文件夹映射，linux一样。
