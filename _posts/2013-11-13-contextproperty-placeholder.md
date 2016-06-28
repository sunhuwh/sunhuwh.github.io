---
layout: post
title: context:property-placeholder
date: 2013-11-13 15:19
categories: [Spring]
tags: []
---
这个在spring中配置文件中是非常常用的。
context:property-placeholder大大的方便了我们数据库的配置。


```html
只需要在spring的配置文件里添加一句：<context:property-placeholder?location="classpath:jdbc.properties"/>?即可，这里location值为参数配置文件的位置，参数配置文件通常放在src目录下，而参数配置文件的格式跟java通用的参数配置文件相同，即键值对的形式，例如：

#jdbc配置

test.jdbc.driverClassName=com.mysql.jdbc.Driver
test.jdbc.url=jdbc:mysql://localhost:3306/test
test.jdbc.username=root
test.jdbc.password=root
```

这样一来就可以为spring配置的bean的属性设置值了，比如spring有一个jdbc数据源的类DriverManagerDataSource在配置文件里这么定义bean：
<bean id="testDataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
<property name="driverClassName" value="${test.jdbc.driverClassName}"/>
<property name="url" value="${test.jdbc.url}"/>
<property name="username" value="${test.jdbc.username}"/>
<property name="password" value="${test.jdbc.password}"/>
</bean>
这样修改起来也方便，也统一的这个规范。
另外需要注意的是，如果遇到下面着着这种问题：
A模块和B模块都分别拥有自己的Spring XML配置，并分别拥有自己的配置文件：
A模块的Spring配置文件如下:

```html
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd">
   <context:property-placeholder location="classpath*:conf/conf_a.properties"/>
   <bean class="com.xxx.aaa.Bean1"
          p:driverClassName="${modulea.jdbc.driverClassName}"
          p:url="${modulea.jdbc.url}"
          p:username="${modulea.jdbc.username}"
          p:password="${modulea.jdbc.password}"/>
</beans>

```
conf/conf_a.properties：

```html
modulea.jdbc.driverClassName=com.mysql.jdbc.Driver
modulea.jdbc.username=cartan
modulea.jdbc.password=superman
modulea.jdbc.url=jdbc:mysql://127.0.0.1:3306/modulea?useUnicode=true&characterEncoding=utf8

```


B模块的Spring配置文件如下:

```html
    <?xml version="1.0" encoding="UTF-8" ?>  
    <beans xmlns="http://www.springframework.org/schema/beans"  
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
           xmlns:context="http://www.springframework.org/schema/context"  
           xmlns:p="http://www.springframework.org/schema/p"  
           xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd  
           http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd">  
       <context:property-placeholder location="classpath*:conf/conf_b.properties"/>  
       <bean class="com.xxx.bbb.Bean1"  
              p:driverClassName="${moduleb.jdbc.driverClassName}"  
              p:url="${moduleb.jdbc.url}"  
              p:username="${moduleb.jdbc.username}"  
              p:password="${moduleb.jdbc.password}"/>  
    </beans>  
```
conf/conf_b.properties：

```html
moduleb.jdbc.driverClassName=com.mysql.jdbc.Driver
moduleb.jdbc.username=cartan
moduleb.jdbc.password=superman
moduleb.jdbc.url=jdbc:mysql://127.0.0.1:3306/modulea?useUnicode=true&characterEncoding=utf8

```

单独运行A模块，或单独运行B模块都是正常的，但将A和B两个模块集成后运行，Spring容器就启动不了了：
Could not resolve placeholder 'moduleb.jdbc.driverClassName' in string value "${moduleb.jdbc.driverClassName}"
原因：Spring容器采用反射扫描的发现机制，在探测到Spring容器中有一个org.springframework.beans.factory.config.PropertyPlaceholderConfigurer的Bean就会停止对剩余PropertyPlaceholderConfigurer的扫描
spring容器中最多只能定义一个context:property-placeholder，不然就出现那种个错误，那如何来解决上面的问题呢？
A和B模块去掉

```html
<context:property-placeholder location="classpath*:conf/conf_b.properties"/> 
```
然后重新写个xml：


```html
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.2.xsd
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.2.xsd">
   <context:property-placeholder location="classpath*:conf/conf*.properties"/>
   <import resource="a.xml"/>
   <import resource="b.xml"/>
</beans>
```
