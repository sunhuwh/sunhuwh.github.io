---
layout: post
title: JdbcTemplate及报错'dataSource' or 'jdbcTemplate' is required
date: 2014-07-07 03:27
categories: [E-learning, Spring, Hibernate]
tags: []
---

```java
@Service("user2Service")
@Transactional
public class User2ServiceImpl implements User2Service{
	
	@Autowired
	private User2Dao user2Dao;

	@Override
	public void save(User user) {
		user2Dao.save(user);
	}

	@Override
	public int countAll() {
		return user2Dao.countAll();
	}
	


}
```



```java
@SuppressWarnings("deprecation")
@Repository("user2Dao")
public class User2DaoImpl extends SimpleJdbcDaoSupport implements User2Dao{
	private static final String INSERT_SQL = "insert into User(name) values(:name)";
	private static final String COUNT_ALL_SQL = "select count(*) from User";
	
	@Override
	public void save(User user) {
		getSimpleJdbcTemplate().update(INSERT_SQL, new BeanPropertySqlParameterSource(user));
		
	}

	@Override
	public int countAll() {
		return getJdbcTemplate().queryForInt(COUNT_ALL_SQL);
	}
} 

```


```java
@Controller
@RequestMapping("/JdbcTemplateTest")
public class JdbcTemplateTestController {
    
	@Autowired
	private User2Service user2Service;
	
	@Autowired
	private UserService userService;
	
	@RequestMapping(method = RequestMethod.GET)
	public void testBestPractice() {
		User user = new User();
		
		user.setName("test");
		//userService.save(user);
		user2Service.save(user);
	    //Assert.assertEquals(1, userService2.countAll());
	}
	
}
```
注意，如果不加上下面注入dataSource就会报错：'dataSource' or 'jdbcTemplate' is required



```html
<bean id="abstractDao" abstract="true">
    	<property name="dataSource" ref="dataSource"/>
	</bean>
	<bean id="user2Dao"
     	class="com.boventech.learning.daoImpl.User2DaoImpl"
    	parent="abstractDao"/> 
```


