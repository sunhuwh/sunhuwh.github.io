---
layout: post
title: Spring Boot Day1--first application
date: 2017-01-20 18:54
categories: [Spring Boot]
tags: [Spring Boot]
---
Spring Boot作为一个目前非常流行的框架，给我们带来了很多的方便：

#### 1.在很短的时间就可以开发项目，着重代码，免于XML的配置（虽然spring目前已经支持免XML配置），但是Spring Boot更为简洁。@EnableAutoConfiguration注解使应用用一种特定的方式进行配置。

现在我们创建一个maven项目:

mvn archetype:generate -DgroupId=com.test.demo -DartifactId=demo -DpackageName=com.test.demo -DarchetypeArtifactId=maven-archetype-webapp

创建的时间有点长

这个时候src/main目录下，可能没有java文件夹，创建一个java文件夹

完成后，修改pom.xml:

    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.test.demo</groupId>
	<artifactId>demo</artifactId>
	<packaging>jar</packaging>
	<version>0.0.1-SNAPSHOT</version>
	<name>netdisk Maven Webapp</name>
	<url>http://maven.apache.org</url>
	<properties>
		<java.version>1.8</java.version>
		<start-class>sample.web.beetl.Application</start-class>
	</properties>
  
	<!-- Inherit defaults from Spring Boot -->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.4.3.RELEASE</version>
	</parent>
  
	<dependencies>
	    <dependency>
	      <groupId>junit</groupId>
	      <artifactId>junit</artifactId>
	      <scope>test</scope>
	    </dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
	  </dependencies>
  
	  <build>
	    <finalName>demo</finalName>
	    <plugins>
			<plugin>
	             <groupId>org.springframework.boot</groupId>
	             <artifactId>spring-boot-maven-plugin</artifactId>
	         </plugin>
	         <plugin>
	             <groupId>org.apache.maven.plugins</groupId>
	             <artifactId>maven-surefire-plugin</artifactId>
	             <configuration>
	                 <useSystemClassLoader>false</useSystemClassLoader>
	             </configuration>
	         </plugin>
		</plugins>
	  </build>
	</project>


创建启动程序：

	import org.springframework.boot.SpringApplication;
	import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
	import org.springframework.web.bind.annotation.*;
	
	@RestController
	@EnableAutoConfiguration
	public class Application {
	
		@RequestMapping("/")
		public String home() {
			return "Hello";
		}
		
		public static void main(String[] args) {
			SpringApplication.run(Application.class, args);
		}
	}


右键，Run As Java Application
 
浏览器访问localhost:8080


注意pom中我配置了一个：<start-class>sample.web.beetl.Application</start-class>

<start-class>中配置的是启动类，在用mvn spring-boot:run运行的时候需要用到这个。启动类需要自己配置。


#### 2.目前微服务非常的流行，而Spring Boot开发微服务非常的快。RestFul，并且可以不用我们自己准备tomcat（等等容器），可以打包成jar包，直接独立运行。

#### 3.各种starter，使得使用起来非常方便，

比如数据库的spring-boot-starter-jdbc，spring-boot-starter-data-jpa...

web项目开发的：spring-boot-starter-web

缓存的：spring-boot-starter-data-redis

安全框架：spring-boot-starter-security

如上面项目中我们使用了spring-boot-starter-web。

看看spring-boot的文档，这个的作用：
	
Starter for building web, including RESTful, applications using Spring MVC. Uses Tomcat as the default embedded container
tomcat，RestFul，springmvc都有


未完待续....