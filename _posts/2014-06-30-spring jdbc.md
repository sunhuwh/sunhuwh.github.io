---
layout: post
title: spring jdbc
date: 2014-06-30 00:17
categories: [E-learning, Spring]
tags: [spring jdbc, jdbc]
---
传统的jdbc非常麻烦，有很多重复，需要考虑很多因素。
现在spring简化了jdbc编程。
spring主要提供了：jdbc模板方式，关系数据库对象化方式，SimpleJdbc方式。三种方式来简化。看看各个方式解决了那些部分：
jdbc模板方式：将需要改变的和不需要改变的分离开。需要改变的用户可以通过回调来实现。
关系数据库对象化方式：将数据库对象化。这样就可以操作对象来代替操作数据库，符合面向对象编程。
SimpleJdbc：实现数据库表插入，存储过程，函数访问。


```java
/**
 * 传统jdbc
 * 不方便，重复，容易出错
 * @author thinkpad
 *
 */
public class JdbcTest {

	/*@Test
	public void test() throws Exception {
	    Connection conn = null;
	    PreparedStatement pstmt = null;
	    try {
	      conn = getConnection();              //1.获取JDBC连接
	      String sql = "select * from INFORMATION_SCHEMA.SYSTEM_TABLES";//2.声明SQL
	      pstmt = conn.prepareStatement(sql);    //3.预编译SQL
	      ResultSet rs = pstmt.executeQuery();   //4.执行SQL
	      process(rs);                       //5.处理结果集
	      closeResultSet(rs);                 //5.释放结果集
	      closeStatement(pstmt);              //6.释放Statement
	      conn.commit();                    //7.提交事务
	    } catch (Exception e) {//8.处理异常并回滚事务
	      
	      conn.rollback();
	      throw e;
	    } finally {
	      closeConnection(conn);//9.释放JDBC连接，防止JDBC连接不关闭造成的内存泄漏
	    }
	}*/

}
```
![](http://sishuok.com/forum/upload/2012/2/22/92e26629cf94f0abce8b334f005312c5__1.JPG)

