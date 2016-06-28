---
layout: post
title: http content-type
date: 2014-05-06 20:59
categories: [简单学习网, java]
tags: []
---
方法：
写个mime.properties：


```html
png=image/png
gif=image/gif
ief=image/ief
jpe=image/jpeg
jpeg=image/jpeg
```

这个是当知道后缀的时候可以获取对应的content-type
MIMEPropertiesReader.java


```java
public class MIMEPropertiesReader {
	
	private static Properties properties=null;

	private static final String FILE_NAME="mime.properties";

	private MIMEPropertiesReader() {}
	
	static{
		if (null == properties) {
			properties = new Properties();
			ClassLoader classLoader = Renders.class.getClassLoader();
			InputStream inputStream = classLoader.getResourceAsStream(FILE_NAME);
			try {
				properties.load(inputStream);
			} catch (IOException e) {
				e.printStackTrace();
			}finally{
				if(null!=inputStream){
					try {
						inputStream.close();
					} catch (IOException e) {
						e.printStackTrace();
					}
				}
			}
		}
	}
	
	public static String getProperty(String property) {
		return properties.getProperty(property);
	}
}

```



```java
 String[] f =  file.getPath().split("\\.");
        String contentType = f[f.length-1].toLowerCase();
        contentType = MIMEPropertiesReader.getProperty(contentType);
```

这样就获取到了
   