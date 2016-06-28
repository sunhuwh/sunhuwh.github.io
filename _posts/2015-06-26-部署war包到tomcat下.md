---
layout: post
title: 部署war包到tomcat下
date: 2015-06-26 18:22
categories: [tomcat, maven]
tags: [命令]
---
#部署war包到tomcat下
***
##MVN
-先用mvn命令，mvn package打包
如果想打包过程中跳过测试，采用：mvn package -Dmaven.test.skip=true
##tomcat下操作
- 找到tomcat路径，tomcat。
- 将war包拷到tomcat\webapps下，然后tomcat\bin\startup.bat。启动tomcat。这时会发现tomcat\webapps下多了一个发布的文件。（如果需要改变其中的文件，改后再重启tomcat）

