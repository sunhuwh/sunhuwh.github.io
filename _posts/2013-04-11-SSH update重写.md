---
layout: post
title: SSH update重写
date: 2013-04-11 12:35
categories: [SSH]
tags: []
---
原本以为我的update功能真的完成了，但是从浏览器上看是修改了，而从mysql-Front上一看，什么都没变动。
错误所在，我以为hibernate的insert和update是一样的，只用session.save(object)就可以了，但是update却是需要save后再加session.beginTransaction().commint();这个以后一定得记住！！！
如果如果我在SSH底层Dao的方法中update添加参数Object object，那么我在使用这个方法时，比如我有个类Content（与数据库的表相对应的类），然后在Action中new了一个对象theContent，并且object定义的就是这个对象，那么在下面接下来，update方法中的object表示的含义就是theContent了。
   