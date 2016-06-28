---
layout: post
title: JFreeChart改变柱子的宽度，柱子上显示值，图片自适应大小
date: 2013-09-12 22:54
categories: [JFreeChart]
tags: []
---
加了这个：
BarRenderer barrenderer = new BarRenderer();
barrenderer.setMaximumBarWidth(0.1);
barrenderer.setMinimumBarLength(0.1);
但是却没有效果，后来找来找去，原因竟然是没写这句话：
plot.setRenderer(renderer);

柱子上加对应数值：
CategoryPlot plot = (CategoryPlot) chart.getCategoryPlot();
BarRenderer customBarRenderer = (BarRenderer) plot.getRenderer();
customBarRenderer.setBaseItemLabelGenerator(new StandardCategoryItemLabelGenerator());//显示每个柱的数值
customBarRenderer.setBaseItemLabelsVisible(true);

图片自适应大小：
加个<div>就行了
