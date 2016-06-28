---
layout: post
title: Junit中使用request（spring）
date: 2015-10-11 23:58
categories: [Spring, java]
tags: [spring, junit]
---
@Before
public void before(){
RequestContextListener listener = new RequestContextListener();
context = new MockServletContext();
request = new MockHttpServletRequest(context);
listener.requestInitialized(new ServletRequestEvent(context, request));
Member member = memberService.findById(Long.valueOf(1));
session = new MockHttpSession();
session.setAttribute(Constants.LOGIN_SESSION_NAME, member.getId());
session.setAttribute(Constants.SESSION_USER, member);
request.setSession(session);
}
