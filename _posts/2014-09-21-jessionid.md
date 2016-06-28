---
layout: post
title: jessionid
date: 2014-09-21 23:18
categories: [E-learning, java]
tags: []
---
jessionid通过这样的方式来从客户端传递到服务器端,从而来标识session。
注意一点，jsessionid跟一般的url参数传递方式是不同的，不是作为参数跟在"？"后面，而是紧跟在url后面用"；"来分隔。
这样在用户禁用cookie的时候我们也可以传递jsessionid来使用session了，
只不过需要每次都把jseesionid作为参数跟在url后面传递。
那这样岂不是很麻烦，每次请求一个url都要判断cookie是否可用，
如果禁用了cookie，还要从url里解析出jsessionid，然后跟在处理完后转到的url后面，以保持jsessionid的传递。
这些问题sun当然已经帮我们想到了。
所以提供了2个方法来使事情变得简单：response.encodeURL()和response.encodeRedirectURL()。
这2个方法会判断cookie是否可用，如果禁用了会解析出url中的jsessionid，并连接到指定的url后面，如果没有找到jessionid会自动帮我们生成一个。
至于为什么要有2个方法？这2个方法有什么不同？google了一下，说是这2个方法在判断是否要包含jsessionid的逻辑上会稍有不同。
在调用HttpServletResponse.sendRedirect前，应该先调用encodeRedirectURL()方法，否则可能会丢失Sesssion信息。
这2个方法的使用方法如：response.sendRedirect(response.encodeURL("/myapp/input.jsp"));。
如果cookie没有禁用，我们在浏览器地址栏中看到的地址是这样的：/myapp/input.jsp，如果禁用了cookie，我们会看到：/myapp/input.jsp;jsessionid=73E6B2470C91A433A6698C7681FD44F4。
所以，我们在写web应用的时候，为了保险起见，应该在程序里的每一个跳转url上都使用这2个方法，来保证session的可用性。