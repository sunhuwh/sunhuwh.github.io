---
layout: post
title: maven+eclipse操作
date: 2013-04-01 12:28
categories: [maven]
tags: []
---
警告：The tag handler class for "s:form" (org.apache.struts2.views.jsp.ui.FormTag) was not found on the Java Build Path
这个问题终于可以解决了， 在我出问题的页面  <s:form> 标签前后删除空格后保存文件 警告即可消失

D:\webblog\.metadata\.plugins\org.eclipse.wst.server.core\该目录是真正的项目目录。

用maven命令创建项目：mvn archetype:create -DgroupId=com.mycompany.app -DartifactId=simple-webapp -DpackageName=com.mycompany.app -DarchetypeArtifactId=maven-archetype-webapp

使用maven的注意事项：
我是用eclipse的maven插件来做的项目，在做的时候遇到了种种问题，如The tag handler class for "s:form" (org.apache.struts2.views.jsp.ui.FormTag) was not found on the Java Build Path
还有就是找不到监听器类等等错误。
针对这些错误，我们需要提前理解下面这些个原理：
每一个工作区都会有一个 .metadata 文件夹，org.eclipse.wst.server.core 就是项目运行的目录， tmp2  3  4 就是你的不同的server。
wtpwebappsz中找到我们的项目，里面会是真正的项目结构，对比脑海中本来应该的目录结构，看是否有差异。
我这样做的：
eclipse中，file->new->other->maven->maven project->选这个：
![](http://img.my.csdn.net/uploads/201304/01/1364791039_1405.png)

![](http://img.my.csdn.net/uploads/201304/01/1364791002_7912.png)

这时我们还得将这个项目变个样子（让他能够支持run as on a server（Tomact）），项目名->properties->project Facets->选中下面的，看清楚版本，然后apply->finish

![](http://img.my.csdn.net/uploads/201304/03/1364972240_3914.png)



然后再删除（只删除eclipse上的，原文件还是保留）你的文件，接着cmd，进你的项目，mvn eclipse:eclipse。再导入项目。



现在我们来改下pom.xml,<packaging>jar</packaging>改为war，因为有了它只需要把war文件放到tomcat就可以运行了。接着就在<dependency>中添加所需的jar


```html
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.mycomply.app</groupId>
  <artifactId>test3-webapp</artifactId>
  <packaging>war</packaging>
  <version>0.0.1-SNAPSHOT</version>
  <name>test21 Maven Webapp</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-asm</artifactId>
      <version>3.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>3.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>3.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>3.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>3.0.5.RELEASE</version>
      <exclusions>
        <!-- Exclude Commons Logging in favor of SLF4j -->
        <exclusion>
          <groupId>commons-logging</groupId>
          <artifactId>commons-logging</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>3.0.5.RELEASE</version>
    </dependency>
    <dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <version>1.2.2</version>
    </dependency>
    <dependency>
      <groupId>javassist</groupId>
      <artifactId>javassist</artifactId>
      <version>3.11.0.GA</version>
    </dependency>
    <dependency>
      <groupId>ognl</groupId>
      <artifactId>ognl</artifactId>
      <version>3.0.5</version>
    </dependency>
    <dependency>
      <groupId>org.freemarker</groupId>
      <artifactId>freemarker</artifactId>
      <version>2.3.19</version>
    </dependency>
    <dependency>
      <groupId>org.apache.commons</groupId>
      <artifactId>commons-lang3</artifactId>
      <version>3.1</version>
    </dependency>
    <dependency>
      <groupId>org.apache.struts.xwork</groupId>
      <artifactId>xwork-core</artifactId>
      <version>2.3.7</version>
    </dependency>
    
    <dependency>
      <groupId>org.apache.struts</groupId>
      <artifactId>struts2-core</artifactId>
      <version>2.3.7</version>
    </dependency>
    <dependency>
      <groupId>org.apache.struts</groupId>
      <artifactId>struts2-spring-plugin</artifactId>
      <version>2.3.7</version>
    </dependency>
    <dependency>
      <groupId>commons-logging</groupId>
      <artifactId>commons-logging</artifactId>
      <version>1.1.1</version>
    </dependency>
    
  </dependencies>
  <build>
    <finalName>test21</finalName>
    
    <!-- Build Settings -->
    <resources>
    <resource>
    <filtering>false</filtering>
    <directory>src/main/resources</directory>
    </resource>
    <resource>
    <filtering>false</filtering>
    <directory>src/main/java</directory>
    <includes>
    <include>**</include>
    </includes>
    <excludes>
    <exclude>**/*.java</exclude>
    </excludes>
    </resource>
    </resources>
    <plugins></plugins>
    <pluginManagement>
    <plugins>
    
    <!-- add Eclipse WTP support -->
    <plugin>
    <artifactId>maven-eclipse-plugin</artifactId>
    <configuration>
    <wtpversion>2.0</wtpversion>
    <projectNameTemplate>
    [artifactId]
    </projectNameTemplate>
    </configuration>
    </plugin>
    <plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <configuration>
    <source>1.5</source>
    <target>1.5</target>
    <encoding>UTF-8</encoding>
    <fork>true</fork>
    
    <compilerArguments>
    <nowarn />
    
    
    </compilerArguments>
    <showWarnings>true</showWarnings>
    
    </configuration>
    </plugin>
    </plugins>
    </pluginManagement>
    
  </build>
</project>



```

这时项目名上有个红叉叉，还不晓得是哪里错了，这时：将项目给删掉，别删除原文件，然后再mvn eclipse:eclipse。再导入项目。
下一步：用tomcat的remove and add方法添加项目进去，再debug，方便在.metadata\.plugins\org.eclipse.wst.server.core\中找到现在建项目的文件，然后随之也好看东西加载进去了没有。
Java Resource上有个地球的图标之后就表示可以用那个server了。
