---
layout: post
title: JFreeChart手册
date: 2013-09-12 23:31
categories: [JFreeChart]
tags: []
---
常见的集中图形：
  pie charts (2D and 3D)：饼图（平面和立体）
    bar charts (regular and stacked, with an optional 3D effect)：柱状图
    line and area charts：曲线图
    scatter plots and bubble charts
    time series, high/low/open/close charts and candle stick charts：时序图
    combination charts：复合图
    Pareto charts
    Gantt charts：甘特图

JFreechart与两个包关系蛮大：org.jfree.chart,org.jfree.data。其中前者主要与图形 本身有关，后者与图形显示的数据有关。
 核心类主要有：
           org.jfree.chart.JFreeChart：图表对象，任何类型的图表的最终表现形式都是在该对象进行一些属性的定制。JFreeChart引擎本身提供了一个工厂类用于创建不同类型的图表对象
           org.jfree.data.category.XXXDataSet:数据集对象，用于提供显示图表所用的数据。根据不同类型的图表对应着很多类型的数据集对象类
           org.jfree.chart.plot.XXXPlot：图表区域对象，基本上这个对象决定着什么样式的图表，创建该对象的时候需要Axis、Renderer以及数据集对象的支持
           org.jfree.chart.axis.XXXAxis：用于处理图表的两个轴：纵轴和横轴
           org.jfree.chart.render.XXXRender：负责如何显示一个图表对象
           org.jfree.chart.urls.XXXURLGenerator:用于生成Web图表中每个项目的鼠标点击链接
           XXXXXToolTipGenerator:用于生成图象的帮助提示，不同类型图表对应不同类型的工具提示类

所以在碰见自己遇到的问题的时候，首先需要判断自己属于上面哪种类型的，然后再在api文档中找寻对应的方法进行解决
