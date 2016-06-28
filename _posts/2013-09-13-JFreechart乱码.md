---
layout: post
title: JFreechart乱码
date: 2013-09-13 17:19
categories: [JFreeChart]
tags: []
---
整个图标分成三部分chart   title，chart 的plot还有chart的  legend三个部分需要对他们分别设置字体就对了。
先看解决方法（ 把这几个全部设置了，都搞定了就可以了）：
**标题乱码**
   chart.getTitle().setFont(new Font("宋体", Font.BOLD,12));
**其他**
1. CategoryAxis domainAxis = plot.getDomainAxis();  
2. 

3. // NumberAxis  valueAxis=(NumberAxis) plot.getRangeAxis(); 
4. //有人说这个是水平方向设置的 方法。
5. ValueAxis numberaxis = plot.getRangeAxis();
6.   
7. /*------设置X轴坐标上的文字-----------*/  
8. domainAxis.setTickLabelFont(new Font("sans-serif", Font.PLAIN, 11));   
9.   
10. /*------设置X轴的标题文字------------*/  
11. domainAxis.setLabelFont(new Font("宋体", Font.PLAIN, 12));   
12.   
13. /*------设置Y轴坐标上的文字-----------*/  
14. numberaxis.setTickLabelFont(new Font("sans-serif", Font.PLAIN, 12));   
15.   
16. /*------设置Y轴的标题文字------------*/  
17. numberaxis.setLabelFont(new Font("黑体", Font.PLAIN, 12));   
18.   
19. /*------这句代码解决了底部汉字乱码的问题-----------*/  
20. jfreechart.getLegend().setItemFont(new Font("宋体", Font.PLAIN, 12));  

对于曲线图；
用于下面两种方法得到的来设置设置水平的和垂直的方法是不一样的。
JFreeChart chart = ChartFactory.createTimeSeriesChart("", "时间", "价格", lineDataset, true, true, true);
 
XYPlot plot = (XYPlot) chart.getPlot();  
 垂直的：
ValueAxis valueaxis=plot.getDomainAxis();
valueaxis.setLabelFont(new Font("宋体",Font.BOLD,12));
valueaxis.setTickLabelFont(new Font("宋体",Font.BOLD,12));
水平的：
NumberAxis  valueAxis=(NumberAxis) plot.getRangeAxis();
 valueAxis.setLabelFont(new Font("宋体",Font.BOLD,12));
 
 
 
JFreeChart jfreechart = ChartFactory.createLineChart("‘大豆’别按小时计算拆线图", "时间", "价格", categoryDataset,PlotOrientation.VERTICAL, true, false,false);
 
CategoryPlot plot = (CategoryPlot) jfreechart.getPlot();
 
 CategoryAxis domainaxis=plot.getDomainAxis();
   水平的：
 domainaxis.setLabelFont(new Font("宋体",Font.BOLD,20));
 
 domainaxis.setTickLabelFont(new Font("宋体", Font.PLAIN, 12));
垂直的：
NumberAxis  valueAxis=(NumberAxis) plot.getRangeAxis();
 
 valueAxis.setLabelFont(new Font("宋体",Font.BOLD,20));
 
 
 
**上面的是针对柱状图的，下面的是 设置饼状图的。**
标题：chart.setTitle(new TextTitle("我的标题",new Font("宋体",Font.BOLD,20)));
    
图例： LegendTitle legendtitle=chart.getLegend(0); 
   legendtitle.setItemFont(new Font("我的标题",Font.ITALIC,20));
    
饼上面的文字：
PiePlot plot=(PiePlot)chart.getPlot();
    
    plot.setLabelFont(new Font("宋体",Font.BOLD,20));
原因：
jfreechart主要是用来动态产生各种数据图形的，可最初使用的时候大都会碰到图片中的中文乱码或是一个小方块的情况。

仔细研究主要有以下2种原因：
1：服务器缺少中文字体，这多发生在Hp等unix操作系统上，解决的方法就是下载可用字体库到系统中，
有人也提出在Windows上产生图片在传回到Unix主机上的方法。
2：软件版本问题，jfreechart-1.0.10有人说没有问题，但jfreechart-1.0.11到13都有问题，我用的最新的jfreechart-1.0.13不做设置是有问题的。
究其原因，是它代码的内部设置的字体有问题.
先来跟踪一下它的代码：
JFreeChart chart = ChartFactory.createBarChart(
   "数据统计图",
   "设备号",
   "积累值",
   dataset,
   PlotOrientation.VERTICAL,
   true, true, false
   );
它的原型
public static JFreeChart createBarChart(String title,
                                            String categoryAxisLabel,
                                            String valueAxisLabel,
                                            CategoryDataset dataset,
                                            PlotOrientation orientation,
                                            boolean legend,
                                            boolean tooltips,
                                            boolean urls) {
上面的原型又调用了
   JFreeChart chart = new JFreeChart(title, JFreeChart.DEFAULT_TITLE_FONT,
                plot, legend);
currentTheme.apply(chart);
看看缺省字体的定义： 
public static final Font DEFAULT_TITLE_FONT
            = new Font("SansSerif", Font.BOLD, 18);
看看当前主题currentTheme是什么
private static ChartTheme currentTheme = new StandardChartTheme("JFree");
看它的原型定义
public StandardChartTheme(String name) {
        if (name == null) {
            throw new IllegalArgumentException("Null 'name' argument.");
        }
        this.name = name;
        this.extraLargeFont = new Font("Tahoma", Font.BOLD, 20);
        this.largeFont = new Font("Tahoma", Font.BOLD, 14);
        this.regularFont = new Font("Tahoma", Font.PLAIN, 12);
        this.smallFont = new Font("Tahoma", Font.PLAIN, 10);
……
看到了吧，默认的标题字体是SansSerif，在很多中文系统中是没有这种字体的，这可能是用老外开发开源产品的弊端吧。
首先说标题的乱码吧：
public JFreeChart(String title, Font titleFont, Plot plot,
                      boolean createLegend) {
……
对标题设置的代码：
if (title != null) {
            if (titleFont == null) {
                titleFont = DEFAULT_TITLE_FONT;
            }
            this.title = new TextTitle(title, titleFont);
            this.title.addChangeListener(this);
        }
它使用了默认字体，因此要解决这个问题只要，对标题重新设置字体就可以了。
……
TextTitle textTitle = chart.getTitle();
 
textTitle.setFont(new Font("黑体", Font.PLAIN, 20));   
图例和其它乱码一样处理，更换字体。
CategoryPlot plot = chart.getCategoryPlot();    //获得图表区域对象

CategoryAxis domainAxis = plot.getDomainAxis();
 
domainAxis.setVisible(true);

plot.setDomainAxis(domainAxis);


ValueAxis rAxis = plot.getRangeAxis();


/*------设置X轴坐标上的文字-----------*/
       domainAxis.setTickLabelFont(new Font("宋体",Font.PLAIN,15));
       /*------设置X轴的标题文字------------*/
       domainAxis.setLabelFont(new Font("宋体",Font.PLAIN,15));        
       /*------设置Y轴坐标上的文字-----------*/
       rAxis.setTickLabelFont(new Font("宋体",Font.PLAIN,15));
       /*------设置Y轴的标题文字------------*/
       rAxis.setLabelFont(new Font("黑体",Font.PLAIN,15));
这里需要注意的是，哪里出现了乱码就修改哪里的字体，将字体转换为系统有的就可以了。
另外有人提出将jfreechart源文件里面的涉及到SansSerif字体的地方都替换成中文字体在重新编译，来个一劳永逸，我没有试，不知可不可以，我主要采用了重新设置字体的方法。
 
 
 

本文来自CSDN博客，转载请标明出处：[http://blog.csdn.net/kinble/archive/2009/05/06/4155085.aspx](http://blog.csdn.net/kinble/archive/2009/05/06/4155085.aspx)
