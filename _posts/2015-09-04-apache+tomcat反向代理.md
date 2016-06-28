---
layout: post
title: apache+tomcat反向代理
date: 2015-09-04 23:40
categories: [tomcat, apache]
tags: [apache, tomcat]
---
在实际生产过程中，数据吞吐量大，tomcat压力也随之增大。
如何解决这种问题？
多个tomcat和apache集成，使多个tomcat称为一个集群。
集群系统的好处:
高可靠性：当一台服务器出现故障，可以切换到另一台服务器上进行运作。
高性能：由于有多台服务器，可以将压力缓解。
下面是一个apache+tomca反向代理的例子：
需要修改apache的配置文件。
修改/config/httpd.conf
添加：
	#---------------------start------------------------
	LoadModule proxy_module modules/mod_proxy.so
	LoadModule proxy_ajp_module modules/mod_proxy_ajp.so
	LoadModule rewrite_module modules/mod_rewrite.so
	LoadModule proxy_balancer_module modules/mod_proxy_balancer.so
	LoadModule proxy_connect_module modules/mod_proxy_connect.so
	LoadModule proxy_ftp_module modules/mod_proxy_ftp.so
	LoadModule proxy_http_module modules/mod_proxy_http.so
	LoadModule slotmem_shm_module modules/mod_slotmem_shm.so
	LoadModule speling_module modules/mod_speling.so
	LoadModule proxy_html_module modules/mod_proxy_html.so
	LoadModule lbmethod_byrequests_module modules/mod_lbmethod_byrequests.so
	LoadModule buffer_module modules/mod_buffer.so
	LoadModule cache_module modules/mod_cache.so
	LoadModule cache_disk_module modules/mod_cache_disk.so
	LoadModule xml2enc_module modules/mod_xml2enc.so
	#LoadModule ssl_module modules/mod_ssl.so
	#----------------------end---------------------
	
并将：Include conf/extra/httpd-vhosts.conf注解去掉
修改：httpd-vhosts.conf
注解掉全部，然后加上：
	<VirtualHost *:80> 
	         ServerAdmin hu.sun@hotmail.com 
	         ServerName localhost 
	         ServerAlias localhost 
	         ProxyPass / ajp://127.0.0.1:8009/
	        ProxyPassReverse / ajp://127.0.0.1:8009/
	         ErrorLog "logs/lbtest-error.log" 
	         CustomLog "logs/lbtest-access.log" common 
	</VirtualHost>
注意：这里的8009是与tomcat中:
	<Connectorport="8009"protocol="AJP/1.3"redirectPort="8443" />
一样的。
