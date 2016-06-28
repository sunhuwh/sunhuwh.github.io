---
layout: post
title: tomcat之server.xml
date: 2014-05-05 00:20
categories: [简单学习网, tomcat]
tags: []
---
<?xml version="1.0" encoding="UTF-8"?>
<!--Tomcat Server处理一个http请求的过程(tomcat.5.5.28)
假设来自客户的请求为：
[http://localhost:8080/wsota/index.jsp](http://localhost:8080/wsota/index.jsp)
1) 请求被发送到本机端口8080，被在那里侦听的Coyote HTTP/1.1 Connector获得
2) Connector把该请求交给它所在的Service的Engine来处理，并等待来自Engine的回应
3) Engine获得请求localhost/wsota/wsota_index.jsp，匹配它所拥有的所有虚拟主机Host
4) Engine匹配到名为localhost的Host（即使匹配不到也把请求交给该Host处理，因为该Host被定义为该Engine的默认主机）
5) localhost Host获得请求/wsota/wsota_index.jsp，匹配它所拥有的所有Context
6) Host匹配到路径为/wsota的Context（如果匹配不到就把该请求交给路径名为""的Context去处理）
7) path="/wsota"的Context获得请求/wsota_index.jsp，在它的mapping table中寻找对应的servlet
8) Context匹配到URL PATTERN为*.jsp的servlet，对应于JspServlet类
9) 构造HttpServletRequest对象和HttpServletResponse对象，作为参数调用JspServlet的doGet或doPost方法
10)Context把执行完了之后的HttpServletResponse对象返回给Host
11)Host把HttpServletResponse对象返回给Engine
12)Engine把HttpServletResponse对象返回给Connector
13)Connector把HttpServletResponse对象返回给客户browser
-->
<!--port指定一个端口,这个端口负责监听关闭tomcat的请求,shutdown是关闭的命令字符串即SHUTDOWN，如果telnet localhost 8005之后输入SHUTDOWN就会把tomcat关掉-->
<Server port="8005" shutdown="SHUTDOWN">

<!--一些监听的类-->
<Listener className="org.apache.catalina.core.AprLifecycleListener" />
<Listener className="org.apache.catalina.mbeans.ServerLifecycleListener" />
<Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
<Listener className="org.apache.catalina.storeconfig.StoreConfigLifecycleListener"/>

<!---->
<GlobalNamingResources>
    <Environment name="simpleValue" type="java.lang.Integer" value="30"/>
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
       description="User database that can be updated and saved"
           factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
          pathname="conf/tomcat-users.xml" />
</GlobalNamingResources>

<!--该元素由org.apache.catalina.Service接口定义,它包含一个<Engine>元素,以及一个或多个<Connector>,这些Connector元素共享用同一个Engine元素
   Service是一组Connector的集合它们共用一个Engine来处理所有Connector收到的请求
   name指定service的名字，和conf下的Catalina目录名对应-->
<Service name="Catalina">
    
    <!--Connector表示客户端和service之间的连接
       port是web访问的端口，修改端口在此处，如改成80
       maxHttpHeaderSize是最大的http头文件大小单位字节
       maxThreads是最大可以创建的处理请求的线程数
       minSpareThreads是最小剩余线程数，服务启动创建
       maxSpareThreads是最大剩余线程数
       enableLookups是如果为true，则可以通过调用request.getRemoteHost()进行DNS查询来得到远程客户端的实际主机名，若为false则不进行DNS查询，而是返回其ip地址
       redirectPort是指定服务器正在处理http请求时收到了一个SSL传输请求后重定向的端口号
       acceptCount是指定当所有可以使用的处理请求的线程数都被使用时，可以放到处理队列中的请求数，超过这个数的请求将不予处理，当现有线程已经达到最大数75时，
       为客户请求排队.当队列中请求数超过150时，后来的请求返回Connection refused错误
       connectionTimeout是连接超时，毫秒
       disableUploadTimeout是
-->
    <Connector port="8080" maxHttpHeaderSize="8192"
               maxThreads="150" minSpareThreads="25" maxSpareThreads="75"
               enableLookups="false" redirectPort="8443" acceptCount="100"
               connectionTimeout="20000" disableUploadTimeout="true" />
    <!--Connector元素定义了一个JD Connector,它通过8009端口接收由其它服务器转发过来的请求-->
    <Connector port="8009" 
    enableLookups="false" redirectPort="8443" protocol="AJP/1.3" />
    
    <!--Engine表示指定service中的请求处理机，接收和处理来自Connector的请求,Engine用来处理Connector收到的Http请求
           它将匹配请求和自己的虚拟主机，并把请求转交给对应的Host来处理,默认虚拟主机是localhost
       defaultHost指定缺省的处理请求的主机名，它至少与其中的一个host元素的name属性值是一样的
       Engine可以包含如下元素<Logger>, <Realm>, <Value>, <Host>-->
    <Engine name="Catalina" defaultHost="localhost">
      <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
             resourceName="UserDatabase"/>
      
      <!--Host表示一个虚拟主机
         name指定主机名
         appBase应用程序基本目录，即存放应用程序的目录，启动会对该目录下程序进行加载
         unpackWARs如果为true，则tomcat会自动将WAR文件解压，否则不解压，直接从WAR文件中运行应用程序
         autoDeploy如果为true，则自动部署该目录下的引用程序,动态加载更新里面的项目
         xmlValidation就XML的格式校验
         xmlNamespaceAware-->
      <Host name="localhost" appBase="webapps"
       unpackWARs="true" autoDeploy="true"
       xmlValidation="false" xmlNamespaceAware="false">
          <!--Host下可以有多个Context用来配置应用程序
            path访问引用程序的路径名，“”表示默认localhost:8080直接访问到程序dnionCharts
            docbase表示工程存放地址
            reloadable这个属性非常重要，如果为true，则tomcat会自动检测应用程序的/WEB-INF/lib 和/WEB-INF/classes目录的变化，自动装载新的应用程序，我们可以在不重起tomcat的情况下改变应用程序
            -->
          <Context path="" docBase="d:/dnionCharts" reloadable="true" dubug="0"/>    
      </Host> 
    </Engine>   
</Service>
</Server>
其他一些配置示例
首先介绍下war包的解压和压缩(linux下安装的jdk,jre是没有jar命令的)
把当前目录下的所有文件打包成test.war
jar -cvfM0 test.war ./
-c   创建war包
-v   显示过程信息
-f    
-M
-0   这个是阿拉伯数字，只打包不压缩的意思
解压test.war
jar -xvf test.war
解压到当前目录(现在MyEclipse都可以生成war包，右击项目-export-J2EE WAR file)
tomcat部署项目的几种方式(${catalina.home}表示tomcat安装目录)：
1、在conf\server.xml文件里面找到Host标签，在里面加入<Context path="/chart" docBase="D:/myobject/DnionCharts"/>,通过[http://loalhost:8080/chart](http://loalhost:8080/chart)访问。
2、直接把项目放置在webapps下面，直接访问[http://localhost:8080/](http://localhost:8080/)工程名。
3、在conf\Catalina\localhost目录下新建一个XML文件，XML文件名即是访问工程名字，XML内容如<Context docBase="${catalina.home}/myobject/DnionCharts" privileged="true" />,如果新建的XML文件名字为chart.xml则访问路径为：[http://localhost:8080/chart](http://localhost:8080/chart),这个配置要注意的就是conf\server.xml文件的Host标签的name="localhost"，不然加载不到conf\Catalina\localhost下的XML文件，除非都改名如name="127.0.0.1"，那么chart.xml就放在conf\Catalina\127.0.0.1\目录下。

tomcat的conf下server.xml文件通常情况下是：
<Host name="localhost" appBase="webapps"
       unpackWARs="true" autoDeploy="true"
       xmlValidation="false" xmlNamespaceAware="false">
</Host>
意味着将webapps下的所有工程进行加载，通过工程名来进行访问，但是如果我们需要通过域名或者IP直接访问到工程就必须要设置默认访问工程(有一种就是解压war覆盖ROOT下的文件就可以通过域名或IP访问)，一般工程war或者war解压出来的文件都会放在webapps下，例如如下配置：
<Host name="localhost" appBase="webapps"
       unpackWARs="true" autoDeploy="true"
       xmlValidation="false" xmlNamespaceAware="false">
<Context path="" docBase="DnionCharts"/>
</Host>
此时访问localhost:8080的时候，就会直接访问到DnionCharts这个工程，但是会有个问题，重复加载(大家可以在DnionCharts的web.xml下写个servlet使用init来输出一段话，会输出2次，以前做quartz定时任务是总会做两次)。解决这个问题，我的做法是
解压好的war放到别目录下，如在webapps同级下建立一个myobject目录，把默认工程放置下面，并如下配置(通过域名访问)，另外其他工程也可以放置该目录(要加Context指定，通过域名+path别名访问)或者就放置在webapps下(不需要加Context，用域名+工程名访问)
<Host name="localhost" appBase="webapps"
       unpackWARs="true" autoDeploy="true"
       xmlValidation="false" xmlNamespaceAware="false">
       <Alias>www.mydomain.com</Alias>
       <Context path="" docBase="../myobject/DnionCharts"/>
</Host>
