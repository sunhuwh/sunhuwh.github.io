---
layout: post
title: 关于kindeditor在tomcat和apache下运行的问题
date: 2013-01-13 08:21
categories: [Hibernate]
tags: []
---
昨天晚上遇到一个问题，我记得当初在thinkphp中由于想做一个HTML编辑器，以便于图像的呈现，但是当初弄的时候由于对配置这个东西不是很清楚，就糊里糊涂的弄。但是昨天晚上就不同了，我在网上搜了下，发现其实我现在做的这个项目的一个操作页面，add.jsp（增加博客），其实和当初add.html是一样的。但是为啥就是不能编辑器。我先开始以为是struts2或者eclipse需要配置什么东西。
当初弄thinkphp时，由于thinkphp是用apache作为服务器的，配置apache时我是将网络根目录给设置成了D:/webroot，然后又需要HTML编辑器kindeditor，就将kindeditor给解压到了这个根目录下面去了，又由于上传等配置文件都是默认为php的，所以就没修改了。
但是现在由于是用eclipse来开发，struts2来做框架，而现在我的目录也改变了，是D:/webblog，而这个家伙又是用tomcat来开发的，这事情就大发了，两个服务器，两个端口80 8080，当初的thinkphp项目是用80的端口。这就没办法了，牺牲掉apache吧，将apache的端口修改成8080，记住这时tomact不能处于运行状态，不然就报错的，修改方法：
	开始 - 所有程序 - Apache - Configure Apache Server-Edit the Apache httpd.conf Configuration File
	然后往下找  找到
	#
	#Listen 12.34.56.78:8080
	Listen 8080
	把8080改成80就行了...
	
	。然后再打开apache下面的	 httpd.conf，找到这个东东，#
		# DocumentRoot: The directory out of which you will serve your
		# documents. By default, all requests are taken from this directory, but
		# symbolic links and aliases may be used to point to other locations.
		#
		DocumentRoot，设置吧，还有个
		#
		# This should be changed to whatever you set DocumentRoot to.
		#
		<Directory再设置吧。好，还差个，在tomcat中进行设置，tomcat的server.xml文件，找到这个 
		<!-- A "Connector" represents an endpoint by which requests are received
		         and responses are returned. Documentation at :
		         Java HTTP Connector: /docs/config/http.html (blocking & non-blocking)
		         Java AJP  Connector: /docs/config/ajp.html
		         APR (HTTP/AJP) Connector: /docs/apr.html
		         Define a non-SSL HTTP/1.1 Connector on port 8080
		    -->
		
		修改下面的端口8080，改为80，再搜索
		 <!-- A "Connector" represents an endpoint by which requests are received
		         and responses are returned. Documentation at :
		         Java HTTP Connector: /docs/config/http.html (blocking & non-blocking)
		         Java AJP  Connector: /docs/config/ajp.html
		         APR (HTTP/AJP) Connector: /docs/apr.html
		         Define a non-SSL HTTP/1.1 Connector on port 8080
		    -->
		
		修改appBase成你想要的网络根目录就ok了
		
		apache的根目录随意修不修改，最好修改下，免得和tomact混了。tomcat和apache最好别一起开启了，要用时再开，对以后的配置有好处。
	

