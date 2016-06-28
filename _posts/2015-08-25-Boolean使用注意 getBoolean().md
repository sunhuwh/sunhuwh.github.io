---
layout: post
title: Boolean使用注意 getBoolean()
date: 2015-08-25 23:36
categories: [java]
tags: [boolean, java]
---
getBoolean实际上不是获取boolean值。
当且仅当以参数命名的系统属性存在，且等于 “true” 字符串时，才返回 true。
	//大写的true返回为false，必须是小写的true
	String s1 = "true";
	
	String s2 = new String("true");
	
	//这里将s1存放到Java系统属性中了.
	System.setProperty(s1,"true");
	
	System.setProperty(s2,"true");
	
	//这里从系统属性中获取s1，所以获取到了。
	System.out.println(Boolean.getBoolean(s1));//true
	
	System.out.println(Boolean.getBoolean(s2));//true
还是用这种方式进行获取：
	public static void main(String[] args) {
	
	        Boolean b = null;
	
	        if(Boolean.valueOf(String.valueOf(b)).booleanValue()){
	
	            System.out.println(123);
	
	        }else{
	
	            System.out.println(false);
	
	        }
	
	    }
	
	
