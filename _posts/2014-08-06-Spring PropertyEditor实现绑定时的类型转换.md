---
layout: post
title: Spring PropertyEditor实现绑定时的类型转换
date: 2014-08-06 00:38
categories: [E-learning, Spring]
tags: []
---

```java
public class DataBinderTestModel{
	
	private String username;
	private boolean bool;//Boolean值测试
	private PhoneNumberModel phoneNumber;//String->自定义对象的转换测试
	private Date date;//日期类型测试
	
	public String getUsername() {
		return username;
	}
	public void setUsername(String username) {
		this.username = username;
	}
	public boolean isBool() {
		return bool;
	}
	public void setBool(boolean bool) {
		this.bool = bool;
	}
	public PhoneNumberModel getPhoneNumber() {
		return phoneNumber;
	}
	public void setPhoneNumber(PhoneNumberModel phoneNumber) {
		this.phoneNumber = phoneNumber;
	}
	public Date getDate() {
		return date;
	}
	public void setDate(Date date) {
		this.date = date;
	}
	
}

```



```java
//如格式010-12345678 
public class PhoneNumberModel {
	
	private String areaCode;//区号
	private String phoneNumber;//电话号码
	
	public String getAreaCode() {
		return areaCode;
	}
	public void setAreaCode(String areaCode) {
		this.areaCode = areaCode;
	}
	public String getPhoneNumber() {
		return phoneNumber;
	}
	public void setPhoneNumber(String phoneNumber) {
		this.phoneNumber = phoneNumber;
	}
}
```





```java
/**
 * PropertyEditorSupport：一个PropertyEditor的支持类；
 * setAsText：表示将String——>PhoneNumberModel，根据正则表达式进行转换，如果转换失败抛出异常，则接下来的验证器会进行验证处理；
 * getAsText：表示将PhoneNumberModel——>String。
 * @author thinkpad
 *
 */
public class PhoneNumberEditor extends PropertyEditorSupport{

	Pattern pattern = Pattern.compile("^(\\d{3,4})-(\\d{7,8})$");
	@Override
	public void setAsText(String text) throws IllegalArgumentException {
		if(text == null || !StringUtils.hasLength(text)) {
			setValue(null); //如果没值，设值为null
		}
		Matcher matcher = pattern.matcher(text);
		if(matcher.matches()) {
			PhoneNumberModel phoneNumber = new PhoneNumberModel();
			phoneNumber.setAreaCode(matcher.group(1));
			phoneNumber.setPhoneNumber(matcher.group(2));
			setValue(phoneNumber);
		} else {
			throw new IllegalArgumentException(String.format("类型转换失败，需要格式[010-12345678]，但格式是[%s]", text));
		}
	}
	@Override
	public String getAsText() {
		PhoneNumberModel phoneNumber = ((PhoneNumberModel)getValue());
		return phoneNumber == null ? "" : phoneNumber.getAreaCode() + "-" + phoneNumber.getPhoneNumber();
	}
}
```




```java
/**
 * initBinder:第一个扩展点，初始化数据绑定器，在此处我们注册了两个属性编辑器；
 * CustomDateEditor：自定义的日期编辑器，用于在String<——>日期之间转换；
 * binder.registerCustomEditor(Date.class, dateEditor)：表示如果命令对象是Date类型，则使用dateEditor进行类型转换；
 * PhoneNumberEditor：自定义的电话号码属性编辑器用于在String<——> PhoneNumberModel之间转换；
 * binder.registerCustomEditor(PhoneNumberModel.class, new PhoneNumberEditor())：表示如果命令对象是PhoneNumberModel类型，则使用PhoneNumberEditor进行类型转换；
 * @author thinkpad
 *
 */
@SuppressWarnings("deprecation")
public class DataBinderTestController extends AbstractCommandController {
	public DataBinderTestController() {
		setCommandClass(DataBinderTestModel.class); //设置命令对象
		setCommandName("dataBinderTest");//设置命令对象的名字
	}
	@Override
	protected ModelAndView handle(HttpServletRequest req, HttpServletResponse resp, Object command, BindException errors) throws Exception {
		//输出command对象看看是否绑定正确
		System.out.println(command);
		return new ModelAndView("bindAndValidate/success").addObject("dataBinderTest", command);
	}
	@Override
	protected void initBinder(HttpServletRequest request, ServletRequestDataBinder binder) throws Exception {
		super.initBinder(request, binder);
		//注册自定义的属性编辑器
		//1、日期
		DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		CustomDateEditor dateEditor = new CustomDateEditor(df, true);
		//表示如果命令对象有Date类型的属性，将使用该属性编辑器进行类型转换
		binder.registerCustomEditor(Date.class, dateEditor);
		//自定义的电话号码编辑器
		binder.registerCustomEditor(PhoneNumberModel.class, new PhoneNumberEditor());
	}
}
```


加bean：


```java
<bean name="/dataBind" class="com.boventech.learning.controller.DataBinderTestController"/>
```

/bindAndValidate/success.jsp：


```html
EL phoneNumber:${dataBinderTest.phoneNumber}<br/>
	EL date:${dataBinderTest.date}<br/>
```

最后结果应该是：
EL phoneNumber:com.boventech.learning.entity.PhoneNumberModel@1bb8e19
EL date:Sun Mar 18 16:48:48 CST 2012
改改：



输入地址：
http://localhost:8080/E-learning/dataBind?username=sunhuwh&bool=yes&phoneNumber=010-12345678&date=2012-3-18%2016:48:48



