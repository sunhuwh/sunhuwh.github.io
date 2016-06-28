---
layout: post
title: Java 加载Properties文件的六种方式
date: 2014-09-30 00:29
categories: [E-learning, 工具, java]
tags: []
---
1。使用java.util.Properties类的load()方法
示例： InputStream in = lnew BufferedInputStream(new FileInputStream(name));
Properties p = new Properties();
p.load(in);

2。使用java.util.ResourceBundle类的getBundle()方法
示例： ResourceBundle rb = ResourceBundle.getBundle(name, Locale.getDefault());

3。使用java.util.PropertyResourceBundle类的构造函数
示例： InputStream in = new BufferedInputStream(new FileInputStream(name));
ResourceBundle rb = new PropertyResourceBundle(in);

4。使用class变量的getResourceAsStream()方法
示例： InputStream in = JProperties.class.getResourceAsStream(name);
Properties p = new Properties();
p.load(in);

5。使用class.getClassLoader()所得到的java.lang.ClassLoader的getResourceAsStream()方法
示例： InputStream in = JProperties.class.getClassLoader().getResourceAsStream(name);
Properties p = new Properties();
p.load(in);

6。使用java.lang.ClassLoader类的getSystemResourceAsStream()静态方法
示例： InputStream in = ClassLoader.getSystemResourceAsStream(name);
Properties p = new Properties();
p.load(in);

补充

Servlet中可以使用javax.servlet.ServletContext的getResourceAsStream()方法
示例：InputStream in = context.getResourceAsStream(path);
Properties p = new Properties();
p.load(in);

转载：http://blog.csdn.net/yz394777014/article/details/4330583

