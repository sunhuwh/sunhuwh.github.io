---
layout: post
title: hibernate实体状态
date: 2013-06-26 23:51
categories: [Hibernate]
tags: []
---
一.Hibernate实体状态的定义
1.瞬态：
 一个实体通过new操作符创建后，没有和Hibernate的Session建立关系，也没有手动赋值过该实体的持久化
标识(持久化标识可以认为是映射表的主键)。
 此时该实体中任何属性的更新都不会反映到数据库表中。
2.持久化：
 当一个实体和Hibernate的Session创建了关系，并获取了持久化标识，而且在Hibernate的Session生命周期内
存在。
 此时针对该实体任何属性的更改都会直接影响到数据库表中一条记录对应字段的更新，即与数据库表同步。
3.脱管：
 当一个实体和Hibernate的Session创建了关系，并获取了持久化标识，而此时Hibernate的Session生命周期结
束，实体的持久化标识没有被改动过。
 针对该实体任何属性的修改都不会及时反映到数据库表中。
二.实体状态的代码实现
1.瞬态-->持久化的实现

![](http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockStart.gif)public void test1() {
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Catalogs catalog = new Catalogs();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 设置Catalogs属性，持久化标识id属性在映射表中为自增长，不用设置
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setName("Cosmo's Catalog");
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setStatus(1L);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setType(1L);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Session session = HibernateSessionFactory.getSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Transaction tx = session.beginTransaction();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 瞬时-->持久化的实现，保存Catalogs代表的一条记录到数据库
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session.save(catalog);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 打印结果
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Id:" + catalog.getId());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Name:" + catalog.getName());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Status:" + catalog.getStatus());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Type:" + catalog.getType());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 对持久化的Catalogs进行属性的更新，此时将同步数据库
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setName("方寸心间的目录");
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setType(0L);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setStatus(0L);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 不调用update方法，持久化状态的Catalogs会自动同步数据库
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 打印结果
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Id:" + catalog.getId());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Name:" + catalog.getName());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Status:" + catalog.getStatus());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Type:" + catalog.getType());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 提交事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        tx.commit();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 关闭Hibernate Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        HibernateSessionFactory.closeSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockEnd.gif)    }
2.脱管-->持久化、持久化-->脱管
![](http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockStart.gif)public void test2() {
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 创建Catalogs实例
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Catalogs catalog = new Catalogs();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Session session = HibernateSessionFactory.getSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Transaction tx = session.beginTransaction();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 得到持久化Catalogs,此时Catalogs为持久化状态
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session.load(catalog, new Long(101));
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 提交事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        tx.commit();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 关闭Hibernate Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        HibernateSessionFactory.closeSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 关闭Hibernate Session后Catalogs的状态为脱管状态
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 此时依然能够得到数据库在持久化状态时的数据
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Id:" + catalog.getId());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Name:" + catalog.getName());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Status:" + catalog.getStatus());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Type:" + catalog.getType());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 对Catalogs实体的属性的操作将不影响数据库中主键为101的记录
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setName("我的目录");
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setStatus(1L);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setType(1L);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session = HibernateSessionFactory.getSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        tx = session.beginTransaction();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 从脱管状态到持久化状态的转变，此时将更新数据库中对应主键为101的记录
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session.update(catalog);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 打印结果
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Id:" + catalog.getId());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Name:" + catalog.getName());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Status:" + catalog.getStatus());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Type:" + catalog.getType());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 提交事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        tx.commit();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 关闭Hibernate Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        HibernateSessionFactory.closeSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockEnd.gif)    }
三.持久化方法对状态的影响
1.session.delete()方法
 该方法将已经存在的表记录删除，其所影响的状态是从持久化、脱管状态变为瞬时状态。
![](http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockStart.gif)public void testDelete() {
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 创建Catalogs实例
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Catalogs catalog = new Catalogs();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Session session = HibernateSessionFactory.getSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        Transaction tx = session.beginTransaction();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 得到持久化Catalogs,此时Catalogs为持久化状态
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session.load(catalog, new Long(101));
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 删除持久化状态的Catalogs实体,此时Catalogs实体为瞬时状态。
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session.delete(catalog);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 提交事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        tx.commit();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 关闭Hibernate Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        HibernateSessionFactory.closeSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 由于执行了session.delete()因此Catalogs实体为瞬时状态，在数据库中找不到主键为101的数据
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 此时依然能够显示该实体的属性
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Id:" + catalog.getId());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Name:" + catalog.getName());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Status:" + catalog.getStatus());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Type:" + catalog.getType());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 更新Catalogs实体的持久化标志，使其成为脱管状态
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        catalog.setId(new Long(1));
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Id:" + catalog.getId());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Name:" + catalog.getName());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Status:" + catalog.getStatus());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        System.out.println("----Type:" + catalog.getType());
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session = HibernateSessionFactory.getSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 启动事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        tx = session.beginTransaction();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 调用delete方法将脱管状态的Catalogs实体转变为瞬时状态。
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        session.delete(catalog);
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 提交事务
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        tx.commit();
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        // 关闭Hibernate Session
![](http://www.cnblogs.com/Images/OutliningIndicators/InBlock.gif)        HibernateSessionFactory.closeSession();
![](http://www.cnblogs.com/Images/OutliningIndicators/ExpandedBlockEnd.gif)    } 
2.session.merge()方法
 该方法将修改表中记录，其所需要的实体状态为脱管状态，但是注意，它并不影响调用方法前后的状态，即
该实体依然是脱管状态。
代码省略。
3.session.lock()方法
 它为解决事务处理而使用，它会将实体从脱管状态转变为持久化状态。但是值得注意的是，调用session.lock()
方法后，脱管状态的实体信息不会同步到数据库，而是会从数据库中返回该持久化状态。即使在脱管状态对实体属
性进行了修改，一旦调用了session.lock()方法，这种修改该就成了无效。
代码省略。
4.session.saveOrUpdate()方法
 它是Hibernate提供的既可以新增也可以更新的方法，改方法使实体状态从脱管或瞬时直接变成持久化。
 session.saveOrUpdate()方法对实体的持久化标识非常敏感。当实体持久化标识存在，就回发送update SQL,当持
久化标识不存在，就会发送insert SQL。
代码省略。
总结：
1.瞬时-->脱管状态的方法有以下几种。
a.直接将实体的持久化标识进行改变。
b.调用session.createQuery()方法。
c.调用session.getNameQuery()方法。
d.调用session.createFilter()方法。
e.调用session.createCriteria()方法。
f.调用session.createSQLQuery()方法。
2.瞬时-->持久化状态的方法有以下几种。
a.调用session.save()方法。
b.调用session.saveOrUpdate()方法。
3.脱管-->持久化状态的方法有以下几种。
a.调用session.load()方法。
b.调用session.lock()方法。
c.调用session.update()方法。
d.调用session.saveOrUpdate()方法。
4.脱管-->瞬时状态的方法有以下几种。
a.直接将实体的持久化标识清除。
b.调用session.delete()方法。
5.持久化-->脱管状态的方法：关闭Hibernate Session。
6.持久化-->瞬时状态的方法：调用session.delete()方法。
7.脱管状态-->脱管状态但影响数据库记录的方法：调用session.merge()方法。
