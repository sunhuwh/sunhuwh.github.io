---
layout: post
title: Spring Boot Day2--Configuration
date: 2017-01-22 17:48
categories: [Spring Boot]
tags: [Spring Boot]
---
### 1.@ConfigurationProperties

它可以使一个类具有绑定properties的属性到类的属性上的能力。

for example:

StorageProperties.java:StorageProperties将作为载体，用于承载file_storage.properties里面以file.storage开头的属性。

	@ConfigurationProperties(prefix="file.storage",locations = "classpath:file_storage.properties")
	public class StorageProperties {
	
	    private String location;
	
	    public String getLocation() {
	        return location;
	    }
	
	    public void setLocation(String location) {
	        this.location = location;
	    }
	
	}

file_storage.properties:

	file.storage.location = upload-dir

Test:

	@Autowired
    private StorageProperties storageProperties;
	
	storageProperties.getLocation();


#### 2.Spring Boot  Auto-configuration：

上面我们使用了StorageProperties来作为载体来承载properties，最后给别的对象使用。


而Spring Boot自身提供了许多的Bean用来承载这些，我们可以在spring-boot-autoconfig-x.x.x.RELEASE.jar下面找到，譬如说：

用于文件上传的MultipartAutoConfiguration.class,MultiPartProperties.class

如果我们加了：@EnableConfigurationProperties

那么我们的应用就会支持上传，还有具有别的等等功能。

如果我们不想要上传怎么办？加入下面的语句就好了：

@EnableAutoConfiguration(exclude = {MultipartAutoConfiguration.class})

如果想覆盖MultiPartProperties，例如我们现在要将上传的文件的大小改变一下。

可以在application.properties中加入：

	spring.http.multipart.max-file-size=50MB
	spring.http.multipart.max-request-size=50MB


#### 总结：
spring boot提供了一系列的方案简化我们的配置，让我们能够在没必要配置的情况下就不去配置，没必要写xml的时候就不写xml。大大的简化了开发流程。