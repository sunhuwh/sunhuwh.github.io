---
layout: post
title: <form:errors>使用注意
date: 2015-01-21 00:00
categories: [spring mvc, Jsp, HTML]
tags: []
---
表单验证方法：
利用springmvc的表单验证来做；
首先需要在存的时候要将元素给验证一下：
需要注意的是：
需要给验证的对象加上@Valid，标识。
需要有一个对象存错误信息：BindingResult result
（然后如果是save方法，就需要给个重定向RedirectAttributes ra）


```java
@RequestMapping(method = POST)
    public String save(@PathVariable long typeId, @Valid ExField field, BindingResult result, RedirectAttributes ra) {
        if (exFieldService.checkNameExist(field.getName(), typeId)) {
            result.addError(new FieldError("exField", "name", i18n("Duplicate.field.name")));
        }
        if (result.hasErrors()) {
            ra.addFlashAttribute("field", field);
            ra.addFlashAttribute("org.springframework.validation.BindingResult.exField", result);
            return "redirect:/XX";
        }
        ResourceType resourceType = resourceTypeService.findById(typeId);
        field.setResourceType(resourceType);
        exFieldService.save(field);
        return "redirect:/XX";
    }

```



```java
protected String i18n(String message) {
        return messageSource.getMessage(message, null, null);
    }
```


这里需要注意一下：new FieldError时，第一个参数不能是field；
然后页面上也要注意下：由于我们使用的是<form:errors>，这是springmvc提供的，需要引入：


```html
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
```

比如说验证的是name：


```html
<input type="text" class="form-control" id="name" name="name" value="${field.name }">
<form:errors path="exField.name" cssClass="error" />
```
名字为exField,与new FieldError的对象名称相同。


而如果是修改对象，那么就不用重定向。

