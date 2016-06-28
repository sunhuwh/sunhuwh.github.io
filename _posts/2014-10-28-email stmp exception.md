---
layout: post
title: email stmp exception
date: 2014-10-28 23:27
categories: [java, E-learning]
tags: []
---
用1.4版本：


```html
<dependency>
	<groupId>javax.mail</groupId>
	<artifactId>mail</artifactId>
	<version>1.4</version>
</dependency>
```


```java
@Controller
@RequestMapping("/mail")
public class MailController extends ApplicationController{
	
	private static final Logger LOGGER = LoggerFactory.getLogger(MailController.class);
    
    @Autowired
    private MessageSource messageSource;

    @Autowired
    private MailService mailService;

    @RequestMapping(value="/sendEmail",method=RequestMethod.GET)
    public String sendEmail(String id,HttpServletRequest request){
        String serverName = request.getServerName();
        int remotePort = request.getServerPort();
        String domian = serverName.substring(serverName.indexOf(".") + 1);
        if (serverName.split("\\" + ".").length < 3) {
            domian = serverName;
        }
        String basePath = domian + (remotePort == 80 ? "" : (":" + remotePort))
                + request.getContextPath();
        request.setAttribute("basePath", basePath);
        String name = "tiger";
        Object[] parameters = {name, 1, request.getAttribute("basePath")};
        String to = "764503411@qq.com";
        String subject = i18n("activate.success.subject");
        String content = i18n("activate.success.body", parameters, null);
        sendMailToFetchPassword(to, subject, content);
        return null;
    }
    
    
    protected String i18n(String message) {
        return messageSource.getMessage(message, null, null);
    }
    
    protected String i18n(String message,Object[] prams,Locale locale) {
        return messageSource.getMessage(message, prams, locale);
    }
    
    private void sendMailToFetchPassword(String to,String subject,String content){
        final String _to = to;
        final String _subject = subject;
        final String _content = content;
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    mailService.sendHtmlMail(_to, _subject, _content);
                } catch (MessagingException e) {
                    String msg = String.format("Error when send mail to %s[fetch passwod]", _to);
                    LOGGER.error(msg, e);
                }
            }
        }).start();
    }
}
```


```html
<bean id="mailSender" class="org.springframework.mail.javamail.JavaMailSenderImpl">
        <property name="host" value="***.***.***" />
        <property name="port" value="***" />
        <property name="username" value="***" />
        <property name="password" value="****" />
        <property name="javaMailProperties">
            <props>
                <!-- Use SMTP transport protocol -->
                <prop key="mail.transport.protocol">smtp</prop>
                <!-- Use SMTP-AUTH to authenticate to SMTP server -->
                <prop key="mail.smtp.auth">true</prop>
                <!-- Use TLS to encrypt communication with SMTP server -->
                <prop key="mail.smtp.starttls.enable">true</prop>
                <prop key="mail.debug">false</prop>
            </props>
        </property>
    </bean>
```

