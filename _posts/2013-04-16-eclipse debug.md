---
layout: post
title: eclipse debug
date: 2013-04-16 21:22
categories: [eclipse]
tags: []
---
（F5）step into是单步执行，遇到子函数就进入然后再继续单步执行。
（F6）step over是在单步执行时，在函数内遇到子函数时不会进入子函数中进行单步执行，而是将子函数整个执行完再停止，所以前面所说的单步执行的单步是把整个子函数当成是一步来理解的。
（F7）step return是step over与step into的补充，当我们F5单步执行到子函数内部后，想要将剩余部分给执行完毕就用它。并且它还返回到上一层函数。
（F8）执行到最后。
step filter过滤，一直执行到未设立断点的位置。
resume，重新开始执行debug，并且一直运行直到遇到breakpoint。
hit count设置执行次数，适合程序中的for循环。
inspect检查，运算。执行一个
表达式显示执行值。

watch实时地监控变量的变化。
drop to frame是与F5 Step into一起用的，当使用step into进入到了方法内部的时候，可以使用drop to frame让方法恢复到第一步。
   