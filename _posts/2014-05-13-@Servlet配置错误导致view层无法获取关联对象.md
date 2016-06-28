---
layout: post
title: 注解@Servlet配置错误导致view层无法获取关联对象
date: 2014-05-13 02:13
categories: [XML, spring mvc, Spring, E-learning, servlet]
tags: []
---
因为过滤的时候进入的是OpenEntityManagerInViewFilter 的 doFilterInternal 。
而通过断言发现出错出在filterChain.doFilter(request, response)这里。
filterChain.doFilter(request,response)的意思：
![](http://img.blog.csdn.net/20140512212843343?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3VuaHV3aA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
从上图可以理解，
他的作用是将请求转发给过滤器链上下一个对象。这里的“下”指的是哪里 ？
指的是下一个filter，如果没有filter那就是请求的资源。那么问题很有可能出现在过滤的途中，每个过滤器打断言看下。但filter中没有检查任何问题出来。但这里没有出错，出错时因为no session，没拿到那个对象。思路明显出错。

想想，web.xml配置为什么可行，而注解出错了，何故？最后我用这种方式试了一下，就是用web.xml来替换注解配置。然后在OpenEntityManagerInViewFilter 的 doFilterInternal    处打断点。结果程序刚开始运行的时候就进去了，并且在这个方法上打断点后发现：


```java
protected EntityManagerFactory lookupEntityManagerFactory(HttpServletRequest request) {
		if (this.entityManagerFactory == null) {
			this.entityManagerFactory = lookupEntityManagerFactory();
		}
		return this.entityManagerFactory;
	}
```

entityManagerFactor是no null的。而换成注解配置的话是null的。这说明，初始化错误。servlet初始化时顺序是context- param -> listener -> filter -> servlet 。最后问题基本上确定实在servlet配置中。仔细检查，没错，是servlet配置出错。

```java
WebServlet(asyncSupported=true	//支持异步
			,urlPatterns="/"	//路径
			,loadOnStartup=1	
			,name="root"
			,initParams={		//配置文件路径
							@WebInitParam(name="contextConfigLocation"
											,value="classpath*:**/*Context.xml"
										  )
						}
			)
public class DispatcherServletConfig extends DispatcherServlet{

	private static final long serialVersionUID = 4836536409405911240L;

}
```

而DispatcherServlet初始化的上下文加载的Bean是只对Spring Web MVC有效的Bean，如Controller、HandlerMapping、HandlerAdapter等等，该初始化上下文应该只加载Web相关组件。而ContextLoaderListener初始化的上下文加载的Bean是对于整个应用程序共享的，不管是使用什么表现层技术，一般如DAO层、Service层Bean。
所以如果为了图简便，可以由DispatcherServlet全部加载了。


```java
/**
 * 配置Spring的DispatcherServlet
 */
@WebServlet(asyncSupported=true	//支持异步
			,urlPatterns="/"	//路径
			,loadOnStartup=1	
			,name="root"
			,initParams={		//配置文件路径
							@WebInitParam(name="contextConfigLocation"
									,value=""
								  )
						}
			)
public class DispatcherServletConfig extends DispatcherServlet{

	private static final long serialVersionUID = 4836536409405911240L;

}
```


```java
/**
 * 替代Web.xml 的配置代码
 */
public class DefaultConfigration implements WebApplicationInitializer {

	@Override
	public void onStartup(ServletContext context) throws ServletException {
		context.addListener(new ContextLoaderListener());
		context.addListener(new WebAppRootListener());
		context.setInitParameter("contextConfigLocation", "classpath*:**/*Context.xml");
	}

}
```

可参考图：![](http://sishuok.com/forum/upload/2012/7/21/664811d1be029d66250bfe66d65fbe4f__1.JPG)



