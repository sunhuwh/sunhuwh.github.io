---
layout: post
title: JFreeChart
date: 2013-09-12 22:53
categories: [JFreeChart]
tags: [JFreeChart]
---
JFreeChart，帮助我们做报表的。
需要用到的是JFreeChart包很Jcommon包。
我是用maven来做的，所以：
<!-- jFreeChart -->
<dependency>
      <groupId>jfree</groupId>
      <artifactId>jfreechart</artifactId>
      <version>1.0.9</version>
    </dependency>
    <dependency>
      <groupId>jfree</groupId>
      <artifactId>jcommon</artifactId>
      <version>1.0.9</version>
    </dependency>
加个插件，我也不清楚做什么用的：
<!-- jFreeChart -->
 <plugin>
        <groupId>org.mortbay.jetty</groupId>
        <artifactId>maven-jetty-plugin</artifactId>
        <version>6.1.10</version>
        <configuration>
          <scanIntervalSeconds>2</scanIntervalSeconds>
        </configuration>
      </plugin>
另外要有个好习惯，将依赖的仓库设置进pom.xml中去。以后要需要什么包，就直接进地址去找就行了：
<repository>
<id>spring-release</id>
<name>Spring Maven Release Repository</name>
<url>http://repo.springsource.org/libs-release</url>
</repository>

做它需要用到数据，需要一个报表的模型。
数据的设置一般都是用这种方式：
DefaultCategoryDataset dataset= new DefaultCategoryDataset();
dataset.addValue(xx, xx, xx);
参数：第一个，纵坐标的设置；第二个，是什么种类的横坐标的值；第三个，是横坐标的值。
报表的模型，先做个基础模型出来：
JFreeChart chart = ChartFactory.createBarChart( 
                 "问卷结果", // 图表标题
                 "问题", // 目录轴的显示标签
                 "选择人数", // 数值轴的显示标签
                  dataset, // 数据集
                  PlotOrientation.VERTICAL, // 图表方向：水平、垂直
                  false,  // 是否显示图例(对于简单的柱状图必须是 false)
                  false, // 是否生成工具
                  false  // 是否生成 URL 链接
        ); 
ChartFactory里面有很多不同的报表样子，饼状、柱形、折线....
设置数轴的精确度：
得到chart后：
NumberAxis axis = (NumberAxis)chart.getCategoryPlot().getRangeAxis();
axis.setTickUnit(new NumberTickUnit(1D));
其余的对数轴进行设置的：
CategoryPlot plot = chart.getCategoryPlot();
        ValueAxis rangeAxis = plot.getRangeAxis();
//设置最高的一个 Item 与图片顶端的距离
rangeAxis.setUpperMargin(0.15);
//设置最低的一个 Item 与图片底端的距离
rangeAxis.setLowerMargin(1);
//设置Y轴的最小值
rangeAxis.setLowerBound(0);
其他的设置就只用再参照网上的就行了，都是对chart进行设置的。
还有一个使用规范：
我的是只设置的fileName，
String fileName = ServletUtilities.saveChartAsPNG(chart, 700, 400, null);
使用起来：
<img src="${pageContext.request.contextPath}/DisplayChart?filename=${fileName}" border=0 usemap="#${fileName}">
这个时候有个/DisplayChart，这是因为需要装一个servlet，用于处理JFreeChart的报表。
Web.xml中：
<servlet> 
     <servlet-name>DisplayChart</servlet-name> 
     <servlet-class>org.jfree.chart.servlet.DisplayChart</servlet-class> 
</servlet> 
<servlet-mapping> 
    <servlet-name>DisplayChart</servlet-name> 
    <url-pattern>/DisplayChart</url-pattern> 
</servlet-mapping> 
