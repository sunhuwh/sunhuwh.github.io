---
layout: post
title: HibernateTemplate的原理与hibernate三态
date: 2013-05-01 08:35
categories: [Hibernate]
tags: []
---
由于HibernateTemplate的原理与JdbcTemplate的原理类似，现在先讨论JdbcTemplate，在使用JDBC的时候，总是要处理繁琐的细节，例如Connection、statement的获得，SQLException的处理，Connection、Statement的关闭等问题。
使用Spring提供的org.springframework.jdbc.core.JdbcTemplate类被设计成线程安全，当中提供的一些操作方法封装了类似以上的流程。
要建立JdbcTemplate的实例就必须有一个DataSource对象：
JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
可使用Spring的依赖注入方式。来代替自己实例化。
刚刚看见一个例子，是这样的：
抽象类A中用到HibernateTemplate，一个类B继承了它，然后bean中是这样定义的，将HibernateTemplate直接注入到了子类B中，父类A一样可以使用HibernateTemplate。

超类是被继承的类，即父类。

getGenericSuperclass()和getActualTypeArguments()基本用法：
import java.lang.reflect.ParameterizedType;
public class TT extends TT2<Integer> {
public static void main(String[] args) {
System.out.println(((ParameterizedType)newTT().
getClass().getGenericSuperclass()).getActualTypeArguments()[0]);
}
}
//output：class java.lang.Integer
说明： getGenericSuperclass() 通过反射获取当前类表示的实体（类，接口，基本类型或void）的直接父类的Type，getActualTypeArguments()返回参数数组。
这样就可以利用它们将DAO做成泛型类。然后将其与HibernateTemplate一起使用，来获取对象，如：
entityClass=(ParameterizedType)newTT().getClass().getGenericSuperclass()).getActualTypeArguments()[0]);
Object entity = this.hibernateTemplate.get(entityClass, id);





弄懂几个概念：临时状态、持久状态、游离状态、脱管状态。
临时状态：又被称为瞬时状态，java中很普遍，new了一个对象，这个对象不与Session实例相关联。
持久状态：
持久的实例在数据库中都有对应的记录，并且还有持久化标识。
持久状态都会与Session、Transaction相关联。Session不会将数据给提交到数据库，而是继续持久着，等待Transaction执行commit方法来提交数据。持久化对象才会与数据库同步，持久化对象就被称为脏对象。
将临时状态转化为持久化状态：
1.Session save这个瞬时对象，使其持久化。
2.使用 find(),get(),load() 和 iterater() 待方法查询到的数据对象，将成为持久化对象。
游离状态：
持久化对象脱离了Session的对象，如被Session缓存清空过的对象，还是有对象的。
脱管状态：
本质上和游离状态差不多，只是比瞬时对象多了一个数据库记录标识值 id.，与Session相关联，后session关闭，对象仍然可以继续改变。
持久化对象变成脱管对象：当执行 close() 或 clear(),evict() 之后，持久对象会变为脱管对象。
游离对象变成脱管对象：
 A.调用persist(),实体从游离转变到托管,最后变成持久化状态. 
  B.调用find()或Query执行查询,实体从持久变成托管.
  C.调用refresh(),游离实体将被重新加载,变成托管状态.
  D.调用merge(),将游离实体变成托管实体.


讨论
一．Session.save(user)运行机理;
1.把User对象加入缓存中，成为持久化对象。
2.选用映射文件指定的标识生成ID。
3.在Session清理缓存时执行：在底层生成insert语句，将对象存入数据库中。
如果在session.save()过程中，更改了User的属性，那么最终还是按照最终更改的来算，特别注意的是ID不能被修改。
二．Session.delete(user)
如果user是持久化对象，那么在session清理缓存的时候在底层执行delete操作。
如果user是游离态对象，那么先将user和session关联起来，最后按照user是持久化对象进行操作。
Save和update的区别：
Save是存储一个新的对象。
Update是把一个脱管对象或临时对象更新到数据库中。
Update和merge的区别：
当session中存在相同持久化标识的对象，用户给出的对象覆盖session已有的持久实例。
1.update会抛出异常。
2.使用merge的时候会将新生成的临时对象的属性复制到session已有的持久对象中，执行后临时对象依然是临时对象，持久化对象依然是持久化对象。







根据上面来试着解决下面的问题：
代码1_save：
[java]
super.getHibernateTemplate().save(user);  
         System.out.println("："+user.getId());  

输出1：
[java]
Hibernate: insert into user (userid, userpwd, userques, userans, usermail, integral, grade, sex, realname) values (?, ?, ?, ?, ?, ?, ?, ?, ?)  
：9  

代码2_merge：
[java]
super.getHibernateTemplate().merge(user);  
         System.out.println("："+user.getId());  

输出2
[java]
Hibernate: insert into user (userid, userpwd, userques, userans, usermail, integral, grade, sex, realname) values (?, ?, ?, ?, ?, ?, ?, ?, ?)  
：0  

代码3_merge： 
[java]
user = (User)super.getHibernateTemplate().merge(user);  
         System.out.println("："+user.getId());  

输出3： 
[java]
Hibernate: insert into user (userid, userpwd, userques, userans, usermail, integral, grade, sex, realname) values (?, ?, ?, ?, ?, ?, ?, ?, ?)  
：11  
为什么这几次的输入相差会这么大？
第一次使用了save，那么就会生成一个持久化对象。输出9，正常。
第二次使用了merge后，id为0了。使用merge的时候会将新生成的临时对象的属性复制到session已有的持久对象中，执行后临时对象依然是临时对象。所以这个时候为0.而第三次使用了merge，是这样使用的：user = (User)super.getHibernateTemplate().merge(user); 
这时，访问user.id那么访问的是那个持久化对象的id，而不是上一步那样访问的是临时对象的id。
