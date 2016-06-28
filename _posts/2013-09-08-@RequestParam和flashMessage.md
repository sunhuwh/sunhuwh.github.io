---
layout: post
title: 注解@RequestParam和flashMessage
date: 2013-09-08 18:20
categories: [Java Web]
tags: []
---
@RequestParam的应用，基本是应用到设置默认值。其他的要收集传过来的数据只需要与表单名字相同就行了。

第二个就是我们在添加、删除、编辑什么成功或者失败后应该要有所显示，这时就需要一个FlashMessage来帮助我们完成这些工作。它的工作机制就是：
添加数据的页面中，submit，Controller中将这个数据进行处理后，根据处理结果调用flashMessage类。这时候会碰见一个问题，就是刷新页面后会出现flashMessage处理后的结果。所以在Controller应该要将那个用完后就销毁。
还有第二个，当Controller中return为redirect，这时候因为转向另一个method.......这时我们在第一个Controller中用到flashMessage，在多次进行转向后没起到作用了。这时就需要共享才能使用。
