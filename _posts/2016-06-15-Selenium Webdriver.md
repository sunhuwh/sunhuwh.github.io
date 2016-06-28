---
layout: post
title: Selenium Webdriver
date: 2016-06-15 21:26
categories: [selenium]
tags: [selenium, webdriver]
---
Selenium思维导图：
![这里写图片描述](http://img.blog.csdn.net/20160615213746684 "")
	System.setProperty("webdriver.chrome.driver",
	                "C:/Program Files (x86)/Google/Chrome/Application/chromedriver.exe");
	
	final WebDriver driver = new ChromeDriver();
	
	driver.get(url);
	
	driver.findElement(By.id("login")).sendKeys("xxxx");
	driver.findElement(By.id("password")).sendKeys("xxx");
