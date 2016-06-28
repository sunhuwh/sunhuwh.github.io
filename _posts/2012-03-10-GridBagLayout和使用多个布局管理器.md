---
layout: post
title: GridBagLayout和使用多个布局管理器
date: 2012-03-10 22:16
categories: [java]
tags: []
---
1. GridBagLayout（）是建立一个新的GridBagLayout。
    GridBagConstraints（）是建立一个新的GridBagConstraints对象。
    GridBagConstraints（int gridx,int gridy,int gridwidth,int gridheight,double weightx,double weighty,int anchor,int     fill,insets inset,int ipadx,int ipady)
     一共十一个参数，gridx（行）和gridy（列）用来设置组件的位置，默认常数gridBagConstraint.RELATIVE,表示此组件位于其前组件的右边或下边。
    ·gridwidth（所占的单位长度）和gridheight（高度）默认为1
    ·weight x和weight y；用来设置组件随窗口增大的比例，>0,<1，数字越大，组件越大。
    ·anchor：当两个组件大小不等时，小的相对于大的放哪？一共九个位置，就是CENTER(默认).NORTH,NORTHEAST,MORTHWEST,EAST,WEST,SOUTHEAST,SOUTHWEST.
    ·Fill：当参数所处位置有剩余空间时，此参数设置为将组件填满的方向，4个值NONE(默认）,VERTICAL（竖直）,HORIZONTAL（水平）,BOTH.
    ·insets：设置组件间彼此的间距，4个参数分别上下左右，默认（0,0,0,0,）。
    ·ipadx和ipady：组件离中心的距离，x为竖直，y为水平，组件大小，默认为0.
 2.使用多个布局管理器
   当容器中的组件太多时，一个布局管理器是不够用的，不容易得到想要的复杂布局，但一个容器规定死了只能有一 　个布局管理器，这时我们通过叠加透明容器来实现，这个透明容器就是Panal，给Panal设置一个布局管理器就相当　于多了个布局管理器。Panal就是好，可以作为一个组件在别的容器里，又可以包含别的组件在Panal里。
 
