---
layout: post
title: Eclipse下编辑properties文件的插件 【国际化插件】
date: 2014-07-27 23:59
categories: [eclipse, E-learning]
tags: [properties]
---
[Properties Editor](http://www.oschina.net/p/properties+editor)
Eclipse下编辑properties文件的插件，用来写国际化程序非常方便，自动保存为ASCII码。日本人开发的，所以介绍网页全是日文。
#####UPDATE地址：http://propedit.sourceforge.jp/eclipse/updates
官网首页：[http://propedit.sourceforge.jp/index_en.html](http://propedit.sourceforge.jp/index_en.html)
 
install_en.html：[http://propedit.sourceforge.jp/howto_eclipseplugin_install_en.html](http://propedit.sourceforge.jp/howto_eclipseplugin_install_en.html)
 
Html代码  [![收藏代码](http://syc001.iteye.com/images/icon_star.png)]( "收藏这段代码")1. [ INSTALLATION ]  
2.   
3. Please choose from the screen of Eclipse with "Help" ->"Software Updates" -> "Update Manager". An 'Update Manager' opens.  
4.   
5. In the "Feature Updates" view at the lower left of an 'Update Manager', please carry out the right click of the "Sites to Visit", and create a site bookmark by "New" -> "Site Bookmark...".  
6. - The bookmark to create should input the following "URL" and should push an "Finish" button.  
7. Name: Arbitrary input  
8. URL : http://propedit.sourceforge.jp/eclipse/updates/  
9. Bookmark type: Eclipse update site  
10.   
11. If a site bookmark is created, the bookmark created at the bottom of "Feature Updates" will appear.  
12. A click of "jp.gr.java_conf.ussiy.app.propedit.eclipse.feature.PropertiesEditorFeature x.x.x" displays a preview on a right window. Since the button "Install Now" is in around the lower right, please click.  
13.   
14. Since an installation wizard starts, please click a "Next" button rapidly.  
15.   
16. "You will need to restart the workbench for the changes to take effect. Would you like to restart now?" is displayed. Please reboot Eclipse according to a dialog.  

 安装完成后重启eclipse，即可看到效果；
Eg:rgdba_zh_CN.properties
 
Html代码  [![收藏代码](http://syc001.iteye.com/images/icon_star.png)]( "收藏这段代码")1. login.username=\u7528\u6237\u540d\uff1a  
2. login.password=\u5bc6  \u7801\uff1a  
3. login.login=\u767b\u5f55  
4. welcome.msg=\u6b22\u8fce\u4f60\uff1a{0}  

 如果用openwith->propertiesEditor打开是:
 
Java代码  [![收藏代码](http://syc001.iteye.com/images/icon_star.png)]( "收藏这段代码")1. login.username=用户名：  
2. login.password=密  码：  
3. login.login=登录  
4. welcome.msg=欢迎你：{0}  

 
或者用java自带的native2ascii转换中文；
