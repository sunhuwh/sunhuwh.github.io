---
layout: post
title: Transactional
date: 2015-01-22 22:35
categories: [Spring]
tags: []
---
@Transactional            

所有属性

propagation: 指定事务定义中使用的传播

isolation: 指定事务的隔离级别

timeout: 超时时间

readonly : 如果为true, 事务标致为只读

noRollbackFor: 目标方法可抛出的异常所构成的数组，但通知仍会提交事务

rollbackFor: 异常所构成的数组，如果目标方法抛出了这些异常，通知就会回滚
   