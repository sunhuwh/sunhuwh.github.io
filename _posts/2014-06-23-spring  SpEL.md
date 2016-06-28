---
layout: post
title: spring  SpEL
date: 2014-06-23 00:55
categories: [Spring, E-learning]
tags: []
---

```java
public class SpELTest {
    @Test
    public void helloWorld() {
    	//创建解析器：SpEL使用ExpressionParser接口表示解析器，提供SpelExpressionParser默认实现；
        ExpressionParser parser = new SpelExpressionParser();
        //解析表达式：使用ExpressionParser的parseExpression来解析相应的表达式为Expression对象。
        Expression expression =
    			parser.parseExpression("('Hello' + ' World').concat(#end)");
        System.out.println(expression.getExpressionString());
        //构造上下文：准备比如变量定义等等表达式需要的上下文数据。
        EvaluationContext context = new StandardEvaluationContext();
        context.setVariable("end", "!");
        //求值：通过Expression接口的getValue方法根据上下文获得表达式值。
        System.out.println(expression.getValue(context));
        Assert.assertEquals("Hello World!", expression.getValue(context));
    }
    
    
	
	@Test
	public void testParserContext() {
	    ExpressionParser parser = new SpelExpressionParser();
	    ParserContext parserContext = new ParserContext() {
	        @Override
	         public boolean isTemplate() {
	            return true;
	        }
	        @Override
	        public String getExpressionPrefix() {
	            return "#{";
	        }
	        @Override
	        public String getExpressionSuffix() {
	            return "}";
	        }
	    };
	    String template = "#{'Hello '}#{'World!'}";
	    Expression expression = parser.parseExpression(template, parserContext);
	    System.out.println( expression.getValue());
	    Assert.assertEquals("Hello World!", expression.getValue());
	}
}
```


