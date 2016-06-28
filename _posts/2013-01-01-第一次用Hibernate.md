---
layout: post
title: 第一次用Hibernate
date: 2013-01-01 01:12
categories: [Hibernate]
tags: []
---

1. Hibernate是一个不依赖其他平台的轻量级的中间件，现在到处充斥着通过各种工具使用Hibernate进行开发的教程，如 MyEclipse, Ant, Maven等等，但是去掉这些工具，事实上，Hibernate仍然可以使用的。下面的讲解就是使用这种方法，让大家认识Hibernate。需要的软件有：Eclipse + MySQL + Hibernate。
2. 
3. 1. 准备jar包 
4. 首先作为准备，我们去Hibernate官方网站下载Hibernate jar包。本教程用的是hibernate-distribution-3.3.2.GA-dist， 解压，我们使用的主要有hibernate3.jar 和lib/required里的包，其他的包在需要的时候再进行导入即可。需要特别注意的是，我在这些包里没有找到slf4j-nop-1.5.2.jar这个包，需要自己去下载，不然在使用本教程运行时会抛出找不到一些类的异常。下载的地址可以在baidu或者google里搜索。另外需要数据库驱动程序,
 本教程使用的是MySQL数据库,使用的jar包为mysql-connector-java-5.1.0-bin.jar,你可根据自己的mysql版本等信息选择合适的jar包.
5. 
6. 2. 建立工程 
7. 为了方便，我们使用Eclipse作为开发平台，注意，这里没有使用其他的插件，从这个意义上来说，还是比较纯粹的，呵呵。本贴原创,转载请注明来自historycreator.com
8. 
9. 
10. 2.0 在MySQL中建立数据库,名为event. 
11. 建一表,名为events,包含字段有EVENT_ID,title,EVENT_DATE,类型分别是整型自动增长主键,varchar,timestamp.
12. 
13. 2.1 打开eclipse，建立一个Java Project。导入相关类,包括hibernate3.jar和/lib/required里的所有jar包,加上slf4j-nop-1.5.2.jar和mysql-connector-java-5.1.0-bin.jar.
14. 
15. 2.2 新建一个实体类Event 
16. package com.historycreator.hibernate; 
17. 
18. import java.util.Date; 
19. 
20. publicclass Event {
21. private Long id; 
22. 
23. private String title; 
24. private Date date; 
25. 
26. public Event() {} 
27. 
28. public Long getId() { 
29. return id; 
30. } 
31. 
32. privatevoid setId(Long id) {
33. this.id = id; 
34. } 
35. 
36. public Date getDate() { 
37. return date; 
38. } 
39. 
40. publicvoid setDate(Date date) {
41. this.date = date; 
42. } 
43. 
44. public String getTitle() { 
45. return title; 
46. } 
47. 
48. publicvoid setTitle(String title) {
49. this.title = title; 
50. } 
51. } 
52. 
53. 2.3 在com.historycreator.hibernate下建立配置文件Event.hbm.xml,内容如下
54. <?xml version="1.0" encoding="UTF-8"?>
55. <!DOCTYPE hibernate-mapping PUBLIC 
56. "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
57. "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
58. 
59. <hibernate-mapping package="com.historycreator.hibernate">
60. 
61. <class name="Event" table="EVENTS">
62. <id name="id" column="EVENT_ID">
63. <generator class="native" />
64. </id> 
65. <property name="date" type="timestamp" column="EVENT_DATE" />
66. <property name="title" /> 
67. </class> 
68. 
69. </hibernate-mapping> 
70. 
71. 2.4 在src文件夹,也就是在com同级目录下,建立配置文件hibernate.cfg.xml,内容如下:
72. <?xml version="1.0" encoding="UTF-8"?>
73. <!DOCTYPE hibernate-configuration PUBLIC 
74. "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
75. "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
76. 
77. <hibernate-configuration> 
78. 
79. <session-factory> 
80. 
81. <!-- Database connection settings --> 
82. <property name="connection.driver_class">org.gjt.mm.mysql.Driver</property>
83. <property name="connection.url">jdbc:mysql://localhost/event?useUnicode=true&characterEncoding=gbk</property>
84. <property name="connection.username">root</property>
85. <property name="connection.password">test</property>
86. 
87. <!-- JDBC connection pool (use the built-in) --> 
88. <property name="connection.pool_size">1</property>
89. 
90. <!-- SQL dialect --> 
91. <property name="dialect">org.hibernate.dialect.MySQL5Dialect</property>
92. 
93. <!-- Enable Hibernate's automatic session context management --> 
94. <property name="current_session_context_class">thread</property>
95. 
96. <!-- Disable the second-level cache --> 
97. <property name="cache.provider_class">org.hibernate.cache.NoCacheProvider</property>
98. 
99. <!-- Echo all executed SQL to stdout --> 
100. <property name="show_sql">true</property>
101. 
102. <!-- Drop and re-create the database schema on startup --> 
103. <property name="hbm2ddl.auto">update</property>
104. 
105. <mapping resource="com/historycreator/hibernate/Event.hbm.xml"/>
106. 
107. </session-factory> 
108. 
109. </hibernate-configuration> 
110. 
111. 2.5 建工厂类HibernateUtil 
112. package com.historycreator.hibernate; 
113. 
114. import org.hibernate.SessionFactory; 
115. import org.hibernate.cfg.Configuration;
116. 
117. publicclass HibernateUtil {
118. 
119. privatestaticfinal SessionFactory sessionFactory = buildSessionFactory();
120. 
121. privatestatic SessionFactory buildSessionFactory() {
122. try { 
123. // Create the SessionFactory from hibernate.cfg.xml
124. returnnew Configuration().configure().buildSessionFactory();
125. } 
126. catch (Throwable ex) { 
127. // Make sure you log the exception, as it might be swallowed
128. System.err.println("Initial SessionFactory creation failed." + ex);
129. thrownew ExceptionInInitializerError(ex);
130. } 
131. } 
132. 
133. publicstatic SessionFactory getSessionFactory() {
134. return sessionFactory; 
135. } 
136. 
137. } 
138. 
139. 2.6 建类EventManager 
140. package com.historycreator.hibernate; 
141. 
142. import java.util.Date; 
143. 
144. import org.hibernate.classic.Session; 
145. 
146. publicclass EventManager {
147. 
148. publicstaticvoid main(String[] args) { 
149. EventManager mgr = new EventManager();
150. 
151. mgr.createAndStoreEvent("My Event", new Date()); 
152. 
153. HibernateUtil.getSessionFactory().close(); 
154. } 
155. 
156. privatevoid createAndStoreEvent(String title, Date theDate) {
157. Session session = HibernateUtil.getSessionFactory().getCurrentSession();
158. session.beginTransaction(); 
159. 
160. Event theEvent = new Event(); 
161. theEvent.setTitle(title); 
162. theEvent.setDate(theDate); 
163. session.save(theEvent); 
164. 
165. session.getTransaction().commit(); 
166. 
167. } 
168. 
169. } 
170. 
171. 运行即可.效果就是往数据库中插入了一条记录.





遇到了如下一些问题
 <property name="connection.url">jdbc:mysql://localhost/event?useUnicode=true&characterEncoding=gbk</property> 应该改为
 <property name="connection.url">jdbc:mysql://localhost:3306/event?useUnicode=true&amp;characterEncoding=GBK</property>

 我是直接建java project的，引入包的话就必须在建project时，next->next->再引入包

最要命的个问题是这个例子中要求字段EVENT_DATE类型为DateStream，但是数据库就是不准我用这个类型的，害的我不得不改动，将这个类型改为了String类型的，由于我对java的date不是很熟悉，所以先就改成这样。
我是这样改变的，

```java
package com.historycreator.hibernate;  
  
import java.text.SimpleDateFormat;
import java.util.Date;  
  
public class Event {  
    private Long id;  
  
    private String title;  
    private String date;  
  
    public Event() {}  
  
    public Long getId() {  
        return id;  
    }  
  
    private void setId(Long id) {  
        this.id = id;  
    }  
  
    public String getDate() {  
        return date;  
    }  
  
    public void setDate(String date) {  
    	
    	//Date dates=new Date();
    	
    	//SimpleDateFormat df=new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
    	
    	
    	//String date_time = df.format(dates);
    	this.date=date;
    }  
  
    public String getTitle() {  
        return title;  
    }  
  
    public void setTitle(String title) {  
        this.title = title;  
    }  
}  
```

event.hbm.xml:

```java
<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE hibernate-mapping PUBLIC  
        "-//Hibernate/Hibernate Mapping DTD 3.0//EN"  
        "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">  
  
<hibernate-mapping package="com.historycreator.hibernate">  
  
    <class name="Event" table="EVENTS">  
        <id name="id" column="EVENT_ID">  
            <generator class="native" />  
        </id>  
        <property name="date"  column="EVENT_DATE" />  
        <property name="title" />  
    </class>  
  
</hibernate-mapping> 
```
EventManage.java：

```java
package com.historycreator.hibernate;  
  
import java.util.Date;  
  
import org.hibernate.classic.Session;  
  
public class EventManager {  
  
    public static void main(String[] args) {  
        EventManager mgr = new EventManager();  
  
            mgr.createAndStoreEvent("My Event", "2012-12-12 12:12:12");  
          
            HibernateUtil.getSessionFactory().close();  
    }  
  
    private void createAndStoreEvent(String title, String theDate) {  
        Session session = HibernateUtil.getSessionFactory().getCurrentSession();  
        session.beginTransaction();  
        System.out.print(theDate);
        Event theEvent = new Event();  
        theEvent.setTitle(title);  
        theEvent.setDate(theDate);  
        session.save(theEvent);  
  
        session.getTransaction().commit();         
          
    }  
  
}  
```

hibernate.cfg.xml:

```html
<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE hibernate-configuration PUBLIC  
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"  
        "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">  
  
<hibernate-configuration>  
  
    <session-factory>  
  
        <!-- Database connection settings -->  
        <property name="connection.driver_class">org.gjt.mm.mysql.Driver</property>  
        <property name="connection.url">jdbc:mysql://localhost:3306/event?useUnicode=true&characterEncoding=GBK</property>  
        <property name="connection.username">root</property>  
        <property name="connection.password">123456</property>  
  
        <!-- JDBC connection pool (use the built-in) -->  
        <property name="connection.pool_size">1</property>  
  
        <!-- SQL dialect -->  
        <property name="dialect">org.hibernate.dialect.MySQL5Dialect</property>  
  
        <!-- Enable Hibernate's automatic session context management -->  
        <property name="current_session_context_class">thread</property>  
  
        <!-- Disable the second-level cache  -->  
        <property name="cache.provider_class">org.hibernate.cache.NoCacheProvider</property>  
  
        <!-- Echo all executed SQL to stdout -->  
        <property name="show_sql">true</property>  
  
        <!-- Drop and re-create the database schema on startup -->  
        <property name="hbm2ddl.auto">update</property>  
  
        <mapping resource="com/historycreator/hibernate/Event.hbm.xml"/>  
  
    </session-factory>  
  
</hibernate-configuration>
```


