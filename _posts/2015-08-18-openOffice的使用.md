---
layout: post
title: openOffice的使用
date: 2015-08-18 21:29
categories: [HTTP, java]
tags: [openoffice, windows]
---
OpenOffice使用
windows：下载Apache_OpenOffice_4.1.1_Win_x86_install_zh-CN.exe拷贝到本机上
运行后，在C:\Program Files下找到openOffice目录。
进入program，在此目录下运行命令：soffice -headless -accept=”socket,port=8100;urp;”
linux：用root账号进行安装
将 Apache_OpenOffice_4.1.1_Linux_x86-64_install-deb_zh-CN.tar.gz拷贝到linux下，如：目录为/home/ndct/temp
使用解压缩命令：tar -zxvf 压缩文件名.tar.gz解压文件。得到zh-CN文件夹。
使用命令cd zh-CN/DEBS进入DEBS目录。
执行命令$sudo dpkg -i *.deb进行安装。
执行完后，
cd desktop-integration
sudo dpkg -i openoffice4.1-debian-menus_4.1.1-9775_all.deb
这样openOffice安装完成。
进入openOffice目录：
cd /opt/openOffice4/program
启动openOffice:
soffice –headless –accept=”socket,host=127.0.0.1,port=8100;urp;” –nofirststartwizard &
待研究的：需要将openOffice做成一个远程服务，这样就不用所有的机器都装openOffice了。太多余了。
