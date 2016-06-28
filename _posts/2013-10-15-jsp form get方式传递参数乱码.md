---
layout: post
title: jsp form get方式传递参数乱码
date: 2013-10-15 00:55
categories: [java, Jsp, servlet, eclipse, tomcat]
tags: []
---
tomcat配置修改：

server.xml中<Connector  URIEncoding="GBK"  connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>加了个URIEncoding="GBK"。
jsp中编码应如此：
<%@ page language="java" contentType="text/html; charset=GB2312"
    pageEncoding="UTF-8"%>
这是我的猜测，用这的原理是：<%@ page language="java" contentType="text/html; charset=GB2312"
    pageEncoding="UTF-8"%>编码用GB2312，
tomcat解码GBK。
事实也正是如此，刚才试了一下，不用改tomcat的配置，直接用在controller中进行解码：
 new String(name.getBytes("iso-8859-1"), "gb2312");
当然jsp中使必须得用GB2312的

还有一种方式解决乱码问题，那就是统一编码为utf-8。
数据库设置为utf-8，
服务器设置为utf-8，server.xml  <Connector URIEncoding="UTF-8" connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>
java、jsp编码为utf-8。![]()
jsp页面所有设置也为utf-8。<%@ page language="java" contentType="text/html; charset=UTF-8"  pageEncoding="UTF-8"%>

