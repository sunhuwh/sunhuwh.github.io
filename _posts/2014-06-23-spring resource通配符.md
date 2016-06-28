---
layout: post
title: spring resource通配符
date: 2014-06-23 00:53
categories: [Spring, E-learning]
tags: []
---

```java
public class ResourceBean3Controller{
	
	private Resource resource;
    public Resource getResource() {
        return resource;
    }
    public void setResource(Resource resource) {
        this.resource = resource;
    }
    
    @Test
    public void test() {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("/resourceInject.xml");
        ResourceBean3Controller resourceBean1 = ctx.getBean("resourceBean1", ResourceBean3Controller.class);
        ResourceBean3Controller resourceBean2 = ctx.getBean("resourceBean2", ResourceBean3Controller.class);
        Assert.assertTrue(resourceBean1.getResource() instanceof ClassPathResource);
        Assert.assertTrue(resourceBean2.getResource() instanceof ClassPathResource);
    }
    
    
	/*使用路径通配符加载Resource
	Spring提供了一种更强大的Ant模式通配符匹配，从能一个路径匹配一批资源。
	Ant路径通配符支持“？”、“*”、“**”，注意通配符匹配不包括目录分隔符“/”：
	“?”：匹配一个字符，如“config?.xml”将匹配“config1.xml”；
	“*”：匹配零个或多个字符串，如“cn/config.xml”将匹配“cn/javass/config.xml”，但不匹配匹配“cn/config.xml”；而“cn/config-*.xml”将匹配“cn/config-dao.xml”；
	“**”：匹配路径中的零个或多个目录，如“cn/*config.xml”将匹配“cn /config.xml”，
	也匹配“cn/javass/spring/config.xml”；而“cn/javass/config-**.xml”将匹配“cn/javass/config-dao.xml”，即把“**”当做两个“*”处理。
	*/
    @Test
    public void testClasspathPrefix()  {
    	ApplicationContext ctx = new ClassPathXmlApplicationContext("/resource*.xml");
        ResourceBean3Controller resourceBean1 = ctx.getBean("resourceBean1", ResourceBean3Controller.class);
        ResourceBean3Controller resourceBean2 = ctx.getBean("resourceBean2", ResourceBean3Controller.class);
        Assert.assertTrue(resourceBean1.getResource() instanceof ClassPathResource);
        Assert.assertTrue(resourceBean2.getResource() instanceof ClassPathResource);          
    }
    
    @Test
    public void testAsteriskPrefix () throws IOException {
         ResourcePatternResolver resolver = new PathMatchingResourcePatternResolver();      
         //将加载多个绝对匹配的所有Resource
        //然后进行遍历模式匹配
        Resource[] resources=resolver.getResources("/*.properties");
        if(resources.length>0){
        	System.out.println(123);
        	dumpStream(resources[0]);
        }
        
        Assert.assertTrue(resources.length > 0);
        //将加载多个模式匹配的Resource
        resources = resolver.getResources("/log4j.properties");
        Assert.assertTrue(resources.length > 0);  
    }
    
    private void dumpStream(Resource resource) {
        InputStream is = null;
        try {
            //1.获取文件资源
            is = resource.getInputStream();
            //2.读取资源
            byte[] descBytes = new byte[is.available()];
            is.read(descBytes);
            System.out.println(new String(descBytes));
        } catch (IOException e) {
            e.printStackTrace();
        }
        finally {
            try {
                //3.关闭资源
                is.close();
            } catch (IOException e) {
            }
        }
    }
    
    /**
     * 注入
     */
    @Test
    public void testClasspathPrefix2()  {
    	ApplicationContext ctx = new ClassPathXmlApplicationContext("/bean3Resource*.xml");
        ResourceBean3Controller resourceBean1 = ctx.getBean("resourceBean1", ResourceBean3Controller.class);
        ResourceBean3Controller resourceBean2 = ctx.getBean("resourceBean2", ResourceBean3Controller.class);
        Assert.assertTrue(resourceBean1.getResource() instanceof ClassPathResource);
        Assert.assertTrue(resourceBean2.getResource() instanceof ClassPathResource);          
    }
     
}
```


```html
<!-- Spring提供了一个PropertyEditor “ResourceEditor”用于在注入的字符串和Resource之间进行转换。
	因此可以使用注入方式注入Resource。	 -->
	<bean id="resourceBean1" class="com.boventech.learning.controller.ResourceBean3Controller">
	   <property name="resource" value="log4j.properties"/>
	</bean>
	<bean id="resourceBean2" class="com.boventech.learning.controller.ResourceBean3Controller"> 
		<property name="resource"
		value="classpath:log4j.properties"/>
	</bean>
```


