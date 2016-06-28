---
layout: post
title: CommonsMultipartFile与MultipartFile
date: 2014-12-30 23:08
categories: [Spring]
tags: []
---
这两个得到对象方式不同，
对于MulipartFile，只需要这样就可以了：MultipartFile Filedata, HttpServletRequest request
但是对于CommonsMultipartFile，需要@RequestParam CommonsMultipartFile Filedata, HttpServletRequest request,
不然不会进此方法。
