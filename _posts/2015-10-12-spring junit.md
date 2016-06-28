---
layout: post
title: spring junit
date: 2015-10-12 20:30
categories: [Spring]
tags: [junit, 单元测试, spring]
---
spring提供了一套单元测试，免了我们配置数据库。还有spring的一套配置。
	import org.junit.runner.RunWith;
	import org.springframework.test.context.ContextConfiguration;
	import org.springframework.test.context.junit4.AbstractTransactionalJUnit4SpringContextTests;
	import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;
	import org.springframework.test.context.transaction.TransactionConfiguration;
	import org.springframework.transaction.annotation.Transactional;
	
	@RunWith(SpringJUnit4ClassRunner.class)
	@ContextConfiguration(locations = { "classpath*:**/applicationContext-*.xml" })
	@TransactionConfiguration(transactionManager="transactionManager", defaultRollback=false)
	@Transactional
	public abstract classBasicTestcaseextendsAbstractTransactionalJUnit4SpringContextTests{
	
	
	
	
	}
以后我们只要继承这个方法就可以单元测试了
