---
layout: post
title: Hibernate增删改查
date: 2013-01-04 23:25
categories: [Hibernate]
tags: []
---

mysql中库表News,字段如下
id | int | auto_increment | primary key
title | varchar
content | varchar
date | varchar

1：Hibernate的insert操作
Session session = HibernateSessionFactory.getSession();

News news = new News();
news.setContent("my content");
news.setTitle("my title");
news.setDate("my date"); //news是VO

Transaction trans = session.beginTransaction();
session.save(news); //news是PO
trans.commit(); //任何有关数据库更新的操作都是commit后进数据库的
HibernateSessionFactory.closeSession();

2：Hibernate的update操作
Session session = HibernateSessionFactory.getSession();

News news = new News();
news.setId(103); //id不可少，Hibernate只通过id来查找数据库
news.setContent("update content");
news.setTitle("update title");

Transaction trans = session.beginTransaction();
session.update(news);
trans.commit();
HibernateSessionFactory.closeSession();

注意这里我们更新数据不想对date进行更新，所以没写 setDate ，但Hibernate会认为我们是想把date设置为null，所以如果要更新表中一些字段，最好用下面的方法。

Session session = HibernateSessionFactory.getSession();

Transaction trans = session.beginTransaction();
News news = (News)session.get(News.class, 103); //*****(1)
news.setDate("update date"); //*****(2)
session.save(news); //*****(3)
trans.commit();
HibernateSessionFactory.closeSession();

这里其实对数据库进行了两次操作，(1)时从数据库中把相应纪录查找出来，这里news是一个PO，(2)对PO进行date的更新，其他数据没变，然后(3)保存，由于(1)查出的数据就有title,content，所以保存时候title和content都不会是null。

3：Hibernate的delete操作
Session session = HibernateSessionFactory.getSession();

Transaction trans = session.beginTransaction();
News news = new News();
news.setId(8); //用下面那句效果一样，只是多了句select
// News news = (News)session.get(News.class, 8);

session.delete(news);
trans.commit();
HibernateSessionFactory.closeSession();
注意，只能通过id来删除数据，不能通过title或content来删除，会报缺少标示符错误。

使用hql来删除(可作批量删除)
Session session = HibernateSessionFactory.getSession();
String hql = "delete Billdetail where name>'detailName1'";
Query query = session.createQuery(hql);
int ref = query.executeUpdate();
session.beginTransaction().commit();
System.out.println("delete dates=>"+ref); //操作条数

session.close();


4：Hibernate的select操作

Hibernate的select操作非常丰富，这里写常用的：

1.criteria查询
Session session = HibernateSessionFactory.getSession();

Criteria c = session.createCriteria(News.class);//News是类，所以N大写
c.add(Expression.lt("date", "date5"));
c.add(Expression.between("date", "date1", "date8"));
c.addOrder(Order.desc("date"));

List<News> list = c.list();
for(int i=0;i<list.size();i++)
{
System.out.println(list.get(i).getId()+":"+list.get(i).getDate());
}
HibernateSessionFactory.closeSession();

比较符合面向对象的概念，因为库表和JAVA类已经作了映射关系，注意Hibernate的所有操作都是针对JAVA类的，而不是库表，所以要区分大小写。
上面的查询相当于sql是: select * from news where date < 'date5' and date BETWEEN 'date1' and 'date8' ORDER by date desc;

2.HQL查询
Query query = session.createQuery("from News ");
List<News> list = query.list(); //遍历同上

HQL是Hibernate主推的查询方式，和普通SQL语句也比较接近，但很重要一点不同就是HQL中from后面的是JAVA类名，不是库表名，切忌！！！其它就是如果查询全字段 "select *" 可以省略不写。

当不是查询全字段，或者是从两张表中联合查询数据时，返回的是一个数组：
Session session = HibernateSessionFactory.getSession();

Query query = session.createQuery("select n.id,n.title,u.username from News as n,User u");
List list = query.list();//这里每一行都是一个1维数组
for(int i=0;i<list.size();i++)
{
Object []o = (Object[])list.get(i); //转型为数组
int id = (Integer)o[0]; //和select中顺序的类型相对应,可以是类
String title = (String)o[1];
String username = (String)o[2];
System.out.println("id:"+id+" , "+"title"+title+" , "+username);
}
HibernateSessionFactory.closeSession();

查询结果集的大小(和Hibernate2中稍微有点不同)
(Integer)session.createQuery("select count(*) from User").iterate().next();


3.SqlQuery查询
List<News> list = session.createSQLQuery("select * from News").addEntity(News.class).list();

addEntity 不能忘记，这种查询方式是把查询好的结果放到一个实体中，再遍历操作，不推荐使用。

SqlQuery查询一些字段时候用addScalar:
SQLQuery query = session.createSQLQuery("select id,title from News");
query.addScalar("id", Hibernate.INTEGER); //注册字段类型，同下
query.addScalar("title",new org.hibernate.type.StringType());
List list = query.list();
for(int i=0;i<list.size();i++)
{
Object[] o = (Object[])list.get(i);
int id = (Integer)o[0];
String title = (String)o[1];
System.out.println("id:"+id+" , title:"+title);
}

javabean的属性可以作为命名的查询参数(HQL)
Session session = HibernateSessionFactory.getSession();
Transaction trans = session.beginTransaction()

Query query = session.createQuery("from room in class Room where room.name=:a")
query.setParameter("a", "room1"); //和prepareStatement相似

// Room room1 = new Room();
// room1.setName("room1");
// Query query = session.createQuery("from room in class Room where room.name=:name"); //如果用javabean设置参数来查询，=:name的name一定和Room中对应
// query.setProperties(room1);

List<Room> list = query.list();
for(int i=0;i<list.size();i++)
{
System.out.println(list.get(i).getName()+":"+list.get(i).getDescription());
}

trans.commit();
HibernateSessionFactory.closeSession()

