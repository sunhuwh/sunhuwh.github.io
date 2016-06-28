---
layout: post
title: Exception in thread "main" java.lang.NoSuchMethodError org.apache.poi.poifs.filesystem.POIFSFileSys
date: 2015-02-11 23:29
categories: [java]
tags: []
---
Exception in thread "main" java.lang.NoSuchMethodError: org.apache.poi.poifs.filesystem.POIFSFileSystem.getRoot()Lorg/apache/poi/poifs/filesystem/DirectoryEntry;
原因：poi不能和<dependency>
            <groupId>org.textmining</groupId>
            <artifactId>tm-extractors</artifactId>
            <version>0.4</version>
        </dependency>
一起用
