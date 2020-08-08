---
title: JavaScript基础Ⅱ（持续更新）
date: 2020-08-08 22:50:36
tags:
- JavaScript
---
三十四、DOM
DOM（Document Object Model）：文档对象模型，JS通过DOM来对HTML文档进行操作，要点：；
（1）节点（Node）：构成HTML文档最基本的单元，节点类型：文档节点、元素节点、属性节点、文本节点；
（2）浏览器已经提供文档节点对象（document），是window属性，可在页面中直接使用，文档节点代表整个页面；
（3）通过元素对象的id获取HTML文档中的对象：document.getElementById("对象id名")；
（4）修改按钮的文字：JS中获取到的按钮对象名.innerHTML="文字"；
（5）事件：文档或者浏览器窗口中发生的一些特定的交互瞬间，可以在事件对应的属性中设置一些JS代码，当事件被触发时，代码将会被执行；
（6）给一个对象绑定一个单击事件：
&#8195;&#8195;1）在script标签内，JS获取到的对象名.onclick=function(){}；
&#8195;&#8195;2）在对象所在的标签中使用onclick="函数名()"来绑定，函数代码在script标签中编写；