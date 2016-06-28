---
layout: post
title: spring resource资源
date: 2014-06-22 00:33
categories: [E-learning, Spring]
tags: []
---
    在开发的时候通常会遇见很多处理资源的情况。有URL资源，File资源，等等资源。处理这些资源需要不同的接口，有些麻烦。但是如果将这些资源进行抽象，其实就是：打开资源，读取资源，关闭资源。
    最底层接口InputStreamSource：


```java
/**
*getInputStream：每次调用都将返回一个新鲜的资源对应的java.io. InputStream字节流，调用者在使用完毕后必须关闭该资源。
*/
public interface InputStreamSource {
    InputStream getInputStream() throws IOException;
}
```
    Spring提供了Resource接口以继承它，完成对文件的一些基本操作：


```java
/**
返回当前Resource代表的底层资源是否存在，true表示存在。返回当前Resource代表的底层资源是否可读，true表示可读。返回当前Resource代表的底层资源是否已经打开，如果返回true，则只能被读取一次然后关闭以避免内存泄漏；常见的Resource实现一般返回false。如果当前Resource代表的底层资源能由java.util.URL代表，则返回该URL，否则抛出IOException。getURI：如果当前Resource代表的底层资源能由java.util.URI代表，则返回该URI，否则抛出IOException。 getFile：如果当前Resource代表的底层资源能由java.io.File代表，则返回该File，否则抛出IOException。contentLength：返回当前Resource代表的底层文件资源的长度，一般是值代表的文件资源的长度。lastModified：返回当前Resource代表的底层资源的最后修改时间。createRelative：用于创建相对于当前Resource代表的底层资源的资源，比如当前Resource代表文件资源“d:/test/”则createRelative（“test.txt”）将返回表文件资源“d:/test/test.txt”Resource资源。getFilename：返回当前Resource代表的底层文件资源的文件路径，比如File资源“file://d:/test.txt”将返回“d:/test.txt”，而URL资源http://www.javass.cn将返回“”，因为只返回文件路径。getDescription：返回当前Resource代表的底层资源的描述符，通常就是资源的全路径（实际文件名或实际URL地址）。
*/
public interface Resource extends InputStreamSource {
       boolean exists();
       boolean isReadable();
       boolean isOpen();
       URL getURL() throws IOException;
       URI getURI() throws IOException;
       File getFile() throws IOException;
       long contentLength() throws IOException;
       long lastModified() throws IOException;
       Resource createRelative(String relativePath) throws IOException;
       String getFilename();
       String getDescription();
}
```




```java
public class ResourceController {
	
	/**
	 * byte数组资源
	 * 定义资源，确认资源是否存在，访问资源
	 */
	@Test
	public void testByteArrayResource() {
	Resource resource = new ByteArrayResource("Hello World!".getBytes());
	        if(resource.exists()) {
	            dumpStream(resource);
	        }
	}
	
	/*
	 * 打开资源，读取资源，关闭资源
	 * 这个dumpStream方法可重复使用，
	 * testByteArrayResource，testInputStreamResource，testFileResource都可重复使用它
	 */
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
	 * 字节流
	 */
	@Test
	public void testInputStreamResource() {
	   ByteArrayInputStream bis = new ByteArrayInputStream("Hello World!".getBytes());
	   Resource resource = new InputStreamResource(bis);
	    if(resource.exists()) {
	       dumpStream(resource);
	    }
	    Assert.assertEquals(true, resource.isOpen());
	}
	
	/**
	 * 文件的字节流
	 */
	@Test
	public void testFileResource() {
	File file = new File("d:/test.txt");
	    Resource resource = new FileSystemResource(file);
	    if(resource.exists()) {
	        dumpStream(resource);
	    }
	    Assert.assertEquals(false, resource.isOpen());
	}
	 
	/**
	 * ClassPathResource代表classpath路径的资源，将使用ClassLoader进行加载资源。
	 * ClassPathResource加载资源替代了Class类和ClassLoader类的“getResource(String name)”
	 * 和“getResourceAsStream(String name)”两个加载类路径资源方法
	 * 
	 * @throws IOException
	 */
	@Test
	public void testClasspathResourceByDefaultClassLoader() throws IOException {
		Resource resource = new ClassPathResource("log4j.properties");
	    if(resource.exists()) {
	        dumpStream(resource);
	    }
	    System.out.println("path:" + resource.getFile().getAbsolutePath());
	    Assert.assertEquals(false, resource.isOpen());
	}
	 
	
	/**
	 * 指定ClassLoader进行加载
	 * @throws IOException
	 */
	@Test
	public void testClasspathResourceByClass() throws IOException {
		Class clazz = this.getClass();
	    Resource resource1 = new ClassPathResource("/log4j.properties",clazz);
	    if(resource1.exists()) {
	        dumpStream(resource1);
	    }
	    System.out.println("path:" + resource1.getFile().getAbsolutePath());
	    Assert.assertEquals(false, resource1.isOpen());
	       
	    Resource resource2 = new ClassPathResource("/log4j.properties" , this.getClass());
	    if(resource2.exists()) {
	        dumpStream(resource2);
	    }
	    System.out.println("path:" + resource2.getFile().getAbsolutePath());
	    Assert.assertEquals(false, resource2.isOpen());
	}

}

```



