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
