---
layout: post
title: Kindeditor使用
date: 2016-04-26 11:48
categories: [java]
tags: [kindeditor]
---
kindeditor编辑器，他上传后需要接收一个content-type 为 text/html; charset=UTF-8类型的参数。
如果我们直接使用@ResponseBody是不行的。
必须将返回的结果转成json。
response.setContentType(“text/html; charset=UTF-8”);
