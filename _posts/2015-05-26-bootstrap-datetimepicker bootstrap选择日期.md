---
layout: post
title: bootstrap-datetimepicker bootstrap选择日期
date: 2015-05-26 23:53
categories: [jQuery]
tags: []
---
引用bootstrap-datetimepicker的css和js


```html
<div id="datetimepicker2" class="input-append">
    <input data-format="MM/dd/yyyy HH:mm:ss PP" type="text"></input>
    <span class="add-on">
      <i data-time-icon="icon-time" data-date-icon="icon-calendar">
      </i>
    </span>
  </div>
<script type="text/javascript">
  $(function() {
    $('#datetimepicker2').datetimepicker({
      language: 'en',
      pick12HourFormat: true
    });
  });
</script>
```


