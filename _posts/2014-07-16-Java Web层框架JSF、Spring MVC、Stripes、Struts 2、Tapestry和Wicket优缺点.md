---
layout: post
title: Java Web层框架——JSF、Spring MVC、Stripes、Struts 2、Tapestry和Wicket优缺点
date: 2014-07-16 02:37
categories: [E-learning, Spring]
tags: []
---
**JSF
**优点：
◆Java EE标准，这意味着有很大的市场需求和更多的工作机会
◆上手快速并且相对容易
◆有大量可用的组件库
缺点：
◆大量的JSP标签
◆对REST和安全支持不好
◆没有一个统一的实现。既有SUN的实现，又有Apache的实现——MyFaces。
◆国内的OperaMasks还支持AJAX，以及有开发工具支持
**Spring MVC**
优点：
◆对覆盖绑定（overriding binding）、验证（validation）等提供生命周期管理
◆与许多表示层技术/框架无缝集成：JSP/JSTL、Tiles、Velocity、FreeMarker、Excel、XSL、PDF等
◆便于测试——归功于IoC
缺点：
◆大量的XML配置文件
◆太过灵活——没有公共的父控制器
◆没有内置的Ajax支持
**Stripes
**优点：
◆不需要书写XML配置文件
◆良好的学习文档
◆社区成员很热心
缺点：
◆社区比较小
◆不如其他的项目活跃
◆ActionBean里面的URL是硬编码的
**Struts 2**
优点：
◆架构简单——易于扩展
◆标记库很容易利用FreeMarker或者Velocity来定制
◆基于控制器或者基于页面的导航
缺点：
◆文档组织得很差
◆对新特征过分关注
◆通过Google搜索到的大多是Struts 1.x的文档
**Tapestry
**优点：
◆一旦学会它，将极大地提高生产率
◆HTML模板——对页面设计师非常有利
◆每出一个新版本，都会有大量的创新
缺点：
◆文档过于概念性，不够实用
◆学习曲线陡峭
◆发行周期长——每年都有较大的升级
**Wicket
**优点：
◆对Java开发者有利（不是Web开发者）
◆页面和显示绑定紧密
◆社区活跃——有来自创建者的支持
缺点：
◆HTML模板和Java代码紧挨着
◆需要对OO有较好的理解
◆Wicket逻辑——什么都用Java搞定
接着，Matt通过采访这些框架的作者，与他们讨论各种开源的Java Web框架，并且突出各个框架的长处、听取框架作者对其他框架的看法，希望借此了解这些框架的未来发展方向。
下列是一些被采访者：
JSF:Jacob Hookom
RIFE:Geert Bevin
Seam:Gavin King
Spring MVC:Rob Harrop
Spring Web Flow:Rob Harrop and Keith Donald
Stripes:Tim Fennell
Struts 1:Don Brown
Tapestry:Howard Lewis Ship
Trails:Chris Nelson
Struts 2:Patrick Lightbody
Wicket:Eelco Hillenius
Matt对采访做了如下总结：
*JSF:*
如果你想让web应用具有类似桌面程序的功能性，那么JSF的标准规范和大量第三方组件库的支持值得你 信赖。
*Spring MVC:*
综合了许多不同的技术，这使得它可以被广泛地应用到不同类型的项目中去；它可以被当作web应用开发的一个基础平台。
*Stripes:*
可以被应用到存在大量复杂数据交互的程序中；有强大的类型转换、绑定和验证功能；可以使管理大的复杂表单以及直接映射它们到域对象变得简单……
*Tapestry:*
在中到大型项目中，表现突出（当然，你也可以只把它应用到单个页面上），在这些项目中，你可以通过简单地创建新的组件起到杠杆作用。
*Struts 2:*
通常更适合于那些希望可以真正开始做事并且愿意花费大量时间来学习他们使用的开源工具的小项目组。Struts 2的目标不是那些更喜欢拖放式开发的“扶手椅程序员”。
*Wicket:*
非常适合于这样的内/外部网应用：UI很复杂并且你希望可以充分利用你的开发者资源。
上面的总结，基本是突出了各个框架的长处。然而，哪些又是他们不好的地方呢？
Matt提出了评价一个框架好坏与否的标准：
*◆Ajax支持*
是不是内置了？是否便于使用？
*◆书签能力*
用户能否将某个页面收藏起来并且可以方便地返回到该页面？
*验证*
使用是否简单？是否支持客户端（JavaScript）验证？
*◆可测试性*
脱离容器测试控制器，是否足够简单？
*◆提交和重定向
*框架如何处理重复提交问题？
*◆国际化
*如何支持国际化？控制器利用国际化信息，是否容易？
*◆页面修饰*
框架支持哪种类型的页面修饰/组成机制？
*◆社区和技术支持*
提出问题，能否被快速地、恭敬地回答？
*◆开发工具*
是否有支持这个框架的好的工具，尤其是IDE？
*◆市场需求
*学习了这个框架，它能否帮你找到份工作？
*◆岗位数量*
在dice.com和indeed.com上，对这个框架技能的需求如何？
笔者认为这个评价标准，值得大家借鉴。
然后，Matt按照这些评价标准，对各个框架做了以下阐述：
Ajax支持
◆JSF：没有内置的Ajax支持，需要使用ICEfaces和Ajax4JSF
◆Stripes：没有对应的类库，支持流输出
◆Struts 2：内置Dojo，有用于GWT和JSON的插件
◆Spring MVC：没有对应的类库，需要使用DWR和Spring MVC扩展
◆Tapestry：Tapestry 4.1中，有内置的Dojo
◆Wicket：有Dojo和Script.aculo.us支持
书签能力
◆JSF：可以任意提交——URL甚至不被考虑
◆Stripes：使用约定，但是你可以不加理会
◆Struts 2：有命名空间的概念，这使得收藏某个页面并返回变得容易
◆Spring MVC：允许完全的URL控制
◆Tapestry：依然存在一些丑陋的URL
◆Wicket：允许装配（mount）页面/URL
验证
◆JSF：默认的国际化信息丑陋，但是配置简单
◆Stripes和Wicket：用Java类进行验证——不支持客户端验证
◆Struts 2：使用OGNL完成强大的表达式验证功能；只有在Action上指定了规则，才支持客户端验证。
◆Spring MVC：允许你使用公共验证器——这是一种成熟的解决方案
◆Tapestry：有健壮的验证功能——不需自定义就有漂亮的国际化信息
可测试性
◆Spring MVC和Struts 2：允许利用mocks（例如EasyMock、jMock和Spring Mocks）简单地进行测试
◆Tapestry：测试困难，因为页面类被抽象、具体类被简化
◆JSF：页面类可以方便地被测试，实际上很像Struts 2 中的actions
◆Wicket：有WicketTester——一个强大的解决方案
◆Stripes：有Servlet API Mocks和MockRoundtrip
提交和重定向
解决重复提交问题的最简单方法是：在提交后重定向
◆Spring MVC：允许你将参数加到重定向URL上
◆Stripes、Tapestry和Wicket：有“flash式”的支持
◆Struts 2：需要一个自定义的解决方案
◆JSF：需要一个自定义的解决方案，国际化信息很难加入到页面bean中
国际化
◆JSTL的标签使国际化变得简单；如何将国际化信息放到控制器类中，还没有一个统一的标准。
◆Stripes、Spring MVC和JSF：每个地区使用一个资源绑定文件
◆Struts 2、Tapestry和Wicket：提倡把每个页面/action用到的资源文件分开
◆JSF：需要在每个页面上定义资源绑定信息
◆Tapestry：标签比较可怕
页面修饰
◆Tiles能够用于Struts 2、Spring MVC和JSF中；需要对每个页面进行配置。
◆SiteMesh能够用于所有的这些框架中（不推荐在JSF、Tapestry或者Wicket中使用）；在设置完成后， 只需要很少的维护。
开发工具
◆Spring MVC：Spring IDE，但是只做XML校验，不是一个UI/web工具
◆Struts 2：Eclipse
◆Tapestry：Spindle，对编码者非常有利
◆JSF：众多IDE支持，并且做得越来越好
◆Stripes和Wicket：没有任何官方工具
◆NetBeans目前支持Struts *、JSF（+Facelets）、Tapestry和Wicket，尚不支持Stripes和Spring MVC

市场需求
◆Struts 1：需求依然很大并且被广泛使用
◆Spring MVC：越来越受关注，但大部分是因为Spring框架的一些其他特征
◆JSF：很快地变得流行起来
◆Struts 2：正在获得地盘，但是相关的工作机会很少
◆Tapestry：在过去的数年里，受欢迎程度不断增加
◆Wicket和Stripes：还是未知数
