---
layout: post
title: java7 新特性 Files copy
date: 2016-06-09 10:22
categories: [java]
tags: [Files, Path]
---
	Path targetPath = Paths.get("target url");
	Path sourcePath = Paths.get("source url");
	Files.copy(sourcePath, targetPath, StandardCopyOption.REPLACE_EXISTING);
	
option:
ATOMIC_MOVE 原子性的复制
COPY_ATTRIBUTES 将源文件的文件属性信息复制到目标文件中
REPLACE_EXISTING    替换已存在的文件
