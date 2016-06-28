---
layout: post
title: JsonIgnore
date: 2015-06-11 01:31
categories: [java, json]
tags: [responsebody, JsonIgnore, json]
---
当要将list作为一个json传到前端时有可能会出现死循环。
处理方法：在实体类中对不需要的属性加上@JsonIgnore


