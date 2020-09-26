---
title: html5核心（一）
date: 2020-09-25 23:04:21
tags:
- html
---
一、attribute与property
attribute：html的预定义和自定义属性；
property：js原生对象的直接属性；
每一个预定义的attribute都会有一个对应的property；
布尔值属性：property的属性值是布尔值；
非布尔值属性：property的属性值是非布尔值；
property和attribute同步问题：
&#8195;&#8195;非布尔值属性：任何情况下，property和attribute都同步（实时同步）；
&#8195;&#8195;布尔值属性：
&#8195;&#8195;&#8195;&#8195;（1）改变property时，不会同步attribute；
&#8195;&#8195;&#8195;&#8195;（2）在没有改变property时，attribute会同步property；一旦修改了property，attribute不会同步property；
*浏览器和用户操作也只识别property；

二、canvas
（一）简介
1.概念：canvas（画布），是HTML5新增的元素，可通过JavaScript中的脚本来绘制图形；具有默认的width值（300px）和height值（150px）；
2.不支持IE8及以下的浏览器；而支持canvas元素的浏览器会渲染出canvas的图案，而不支持canvas的浏览器会显示canvas的替代内容（主要是canvas标签内的内容，一般下canvas标签内不需要定义编辑任何标签）；
3.在使用canvas开发时，不要使用css来对canvas进行width和height的定义，不然会对canvas画布的宽高造成压缩和对canvas的内容等比例放缩；
4.在使用canvas时，要找到canvas对应的结点然后通过canvas的getContext()方法来获取它的渲染上下文和绘图功能，getContext()只有一个参数：上下文格式；具体的代码例子：
&#8195;&#8195;var 自定义的canvas参数名=document.getElementById('canvas的id名');
&#8195;&#8195;if(自定义的canvas参数名.getContext){  //必须要检查获取到的canvas元素结点的getContext的支持性，这步一定要有
&#8195;&#8195;&#8195;&#8195;var ctx=自定义的canvas参数名.getContext('2d');
&#8195;&#8195;&#8195;&#8195;}