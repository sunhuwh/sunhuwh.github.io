---
layout: post
title: css+javascript+jquery+prototype+ajax+html5+iis+apache
date: 2013-07-06 00:20
categories: [常识, 笔记]
tags: []
---
CSS是为了统一HTML中各标识的显示属性而存在的。
它的特点就是：精简代码，加快网页访问速度，还有对于搜索引擎有好处。


有许多用HTML实现不了的想法，总结如下：
如何显示弹出框？
如何知道用户在使用什么样的浏览器？
如何在状态条上滚动显示信息？
如何在鼠标落在图像上时改变这个图像？
如何对订单进行计数？
以上这些问题是经常遇到的，而HTML却是无法做到，但是javascript可以。
Javascript是为了解决服务器端语言而存在的，javascript是运行在用户浏览器上的，所以在编写javascript也可以说成是客户端编程。
所以这个时候也会出现一些问题，那就是浏览器的兼容性问题。
不同厂家的浏览器，甚至同一厂家不同版本的浏览器的页面阅读器对javascript语句和一些规则都有不用程度的里就差异。
所以不要理所当然的认为一个浏览器执行得很顺利的代码在另一个浏览器上也一样可以执行的非常顺利。应尽可能多的在别的浏览器上进行测试。
由此可归总为：javascript是为了解决HTML不能实现的目标而存在的，它在用户浏览器上运行，所以有一定的局限性和差异性。



jQuery：jQuery 是一个 JavaScript 库，极大地简化了 JavaScript 编程。
通过 jQuery，您可以选取（查询，query） HTML 元素，并对它们执行“操作”（actions）。
语法：
$(selector).action()
· 美元符号定义 jQuery
· 选择符（selector）“查询”和“查找” HTML 元素
· jQuery 的 action() 执行对元素的操作
如下：
[$(this).hide()](http://www.w3school.com.cn/tiy/t.asp?f=jquery_hide_this)
演示 jQuery hide() 函数，隐藏当前的 HTML 元素。
[$("#test").hide()](http://www.w3school.com.cn/tiy/t.asp?f=jquery_hide_id)
演示 jQuery hide() 函数，隐藏 id="test" 的元素。
[$("p").hide()](http://www.w3school.com.cn/tiy/t.asp?f=jquery_hide_p)
演示 jQuery hide() 函数，隐藏所有 <p> 元素。
[$(".test").hide()](http://www.w3school.com.cn/tiy/t.asp?f=jquery_hide_class)
演示 jQuery hide() 函数，隐藏所有 class="test" 的元素。
上面是元素选择器，下面是属性选择器：
如：
$("[href]") 选取所有带有 href 属性的元素。
$("[href='#']") 选取所有带有 href 值等于 "#" 的元素。
$("[href!='#']") 选取所有带有 href 值不等于 "#" 的元素。
$("[href$='.jpg']") 选取所有 href 值以 ".jpg" 结尾的元素。
jQuery CSS选择器：
jQuery CSS 选择器可用于改变 HTML 元素的 CSS 属性。
下面的例子把所有 p 元素的背景颜色更改为红色：
$("p").css("background-color","red");
如果还有不懂的可以查看http://www.w3school.com.cn/jquery/jquery_ref_selectors.asp
jQuery事件：
jQuery事件就是专门为时间而单独设立的。
通过jQuery中的核心函数来进行处理事件。
当HTML中发生什么事件的时候，就会“触发”函数。
如果想要代码更容易得到维护，则单独立个.js文件放这些jQuery代码。


prototype：

function People(name)
{
this.name=name;
//对象方法
this.Introduce=function(){
alert("My name is "+this.name);
}
}
//类方法
People.Run=function(){
alert("I can run");
}
//原型方法
People.prototype.IntroduceChinese=function(){
alert("我的名字是"+this.name);
}
 
//测试
var p1=new People("Windking");
p1.Introduce();
People.Run();
p1.IntroduceChinese();
结果：
我的名字是Windking
I can run
我的名字是Windking
原因：
原型法的主要思想是，现在有1个类A,我想要创建一个类B,这个类是以A为原型的,并且能进行扩展。我们称B的原型为A。 
javascript中的每个对象都有prototype属性，Javascript中对象的prototype属性的解释是：返回对象类型原型的引用。
A.prototype = new B();
理解prototype不应把它和继承混淆。A的prototype为B的一个实例，可以理解A将B中的方法和属性全部克隆了一遍。A能使用B的方 法和属性。这里强调的是克隆而不是继承。可以出现这种情况：A的prototype是B的实例，同时B的prototype也是A的实例。
可以根据上面来理解下面：
function baseClass()
{
this.showMsg = function()
{
     alert("baseClass::showMsg");   
}
}
function extendClass()
{
}
extendClass.prototype = new baseClass();
var instance = new extendClass();
instance.showMsg(); // 显示baseClass::showMsg
可这样理解extendClass是以baseClass的一个实例为原型克隆创建的
下面：俩方法名相同。
function baseClass()
{
    this.showMsg = function()
    {
        alert("baseClass::showMsg");   
    }
}
function extendClass()
{
    this.showMsg =function ()
    {
        alert("extendClass::showMsg");
    }
}
extendClass.prototype = new baseClass();
var instance = new extendClass();
instance.showMsg();//显示extendClass::showMsg
所以可这样理解，现在本体中找，如果本体没有，那么就到原型中找。
如果必须要到原型中找，那么可以这样，用call
extendClass.prototype = new baseClass();
var instance = new extendClass();


var baseinstance = new baseClass();
baseinstance.showMsg.call(instance);//显示baseClass::showMsg
将instance当做baseinstance来调用，调用它的对象方法showMsg”
利用上面知识认真分析下面：
<script type="text/javascript">
function baseClass()
{
    this.showMsg = function()
    {
        alert("baseClass::showMsg");   
    }
   
    this.baseShowMsg = function()
    {
        alert("baseClass::baseShowMsg");
    }
}
baseClass.showMsg = function()
{
    alert("baseClass::showMsg static");
}
function extendClass()
{
    this.showMsg =function ()
    {
        alert("extendClass::showMsg");
    }
}
extendClass.showMsg = function()
{
    alert("extendClass::showMsg static")
}
extendClass.prototype = new baseClass();
var instance = new extendClass();
instance.showMsg(); //显示extendClass::showMsg
instance.baseShowMsg(); //显示baseClass::baseShowMsg
instance.showMsg(); //显示extendClass::showMsg
baseClass.showMsg.call(instance);//显示baseClass::showMsg static
var baseinstance = new baseClass();
baseinstance.showMsg.call(instance);//显示baseClass::showMsg
</script>





AJAX的全名：Asynchronous JavaScript and XML，意思：异步的 JavaScript 和 XML。
Ajax是在不改变全部页面的情况下实现部分页面进行更新。更明确的说法：
在不重载整个网页的情况下，AJAX 通过后台加载数据，并在网页上进行显示。
前面了解了jQuery，它的目的是为了操作HTML元素。
所以AJAX也可以与jQuery配合，函数：
[http://www.w3school.com.cn/jquery/jquery_ref_ajax.asp](http://www.w3school.com.cn/jquery/jquery_ref_ajax.asp)
[
](http://www.w3school.com.cn/jquery/jquery_ref_ajax.asp)


HTML和HTML5的最大区别就在于HTML5加入了一些新特性：
可以绘画：用<canvas>标签来作为图形容器，用javascript来绘图。
定义视频和声频：<video><audio>标签。
获取位置：getCurrentPosition() 方法来获得用户的位置
增加了输入类型：这个功能可以很好的控制和验证输入类型是否属于自己定义的类型。
添加表单属性：<form><input>增加新属性。



IIS，Internet Information Services，译为Internet信息服务。
对于这个就先了解下它有什么功能，涉及的范围有点广。
IIS（Internet Information Server，互联网信息服务）是一种Web（网页）服务组件，其中包括Web服务器、FTP服务器、NNTP服务器和SMTP服务器，分别用于网页浏览、文件传输、新闻服务和邮件发送等方面，它使得在网络（包括互联网和局域网）上发布信息成了一件很容易的事。


Apache是Web服务器，Web服务器是可以向发出请求的浏览器提供文档的程序。
它的跨平台性、安全性、开源使得其成为了最流行的Web服务器之一。
Apache是一个充满补丁的服务器，不断有人为他进行修补、开发新功能、增加新特性，这也就造成了其流行的原因。它性能稳定、速度快、简单。
