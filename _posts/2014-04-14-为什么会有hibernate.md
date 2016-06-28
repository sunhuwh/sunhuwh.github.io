---
layout: post
title: 为什么会有hibernate
date: 2014-04-14 15:52
categories: [Hibernate]
tags: []
---



```java
public User find(Integer id){
   Connection conn = null;
   PreparedStatement stmt = null;
   try {
      conn = dataSource.getConnection();
      stmt = conn.prepareStatement("SELECT * FROM user where id = ?");
      stmt.setInt(1,id.intValue());
      ResultSet result = stmt.executeQuery();
      if(result.next()){
         Integer i = new Integer(result.getInt(1));
         String name = result.getString(2);
         Integer age = new Integer(result.getInt(3));

         User user = new User();
         user.setId(i);
         user.setName(name);
         user.setAge(age);

         return user;
      }
   }catch (SQLException e){
      e.printStackTrace();
   }
   finally{
      if(stmt!=null){
          try{
              stmt.close();
          }catch(SQLException){
              e.printStackTrace();
          }
      }
      if(conn!=null){
         try{
             conn.close();
         }catch(SQLException e){
             e.printStackTrace();
         }
      }
   }
   return null;
}

```
这是个直接用JDBC查询的一个程序

jdbc(java database connectivity，java数据库连接)的api中的主要的四个类之一的java.sql.statement要求开发者付出大量的时间和精力。 在使用statement获取jdbc访问时所具有的一个共通的问题是输入适当格式的日期和时间戳：2002-02-05 20:56 或者 02/05/02 8:56 pm。 
通过使用java.sql.preparedstatement，这个问题可以自动解决。一个preparedstatement是从 java.sql.connection对象和所提供的sql字符串得到的，sql字符串中包含问号（?），这些问号标明变量的位置，然后提供变量的值， 最后执行语句，例如：
stringsql = "select * from people p where p.id = ? and p.name = ?";
preparedstatement ps = connection.preparestatement(sql);
ps.setint(1,id);
ps.setstring(2,name);
resultset rs = ps.executequery();

Hibernate产生的意义：
1.SQL、JAVA两个完全不同的语言模型，在程序中用SQL很难维护。
2.封装，从数据库中得到的数据必须编写一段程序才能将数据封装成user类的实例。添加则是于此相反的。
3.异常处理，多次try catch。


