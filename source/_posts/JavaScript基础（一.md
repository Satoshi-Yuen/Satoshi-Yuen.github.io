---
title: JavaScript基础Ⅰ（持续更新）
date: 2020-07-13 23:54:03
tags:
- JavaScript
---
在学习JavaScript的时候的一些笔记干货：

一、输出
（1）控制浏览器弹出一个警告框：alert("");
（2）使计算机在body区域中输出内容：document.write("");
（3）向控制台输出一个内容：console.log("");

二、编写位置
（1）button标签的onclick属性内；
（2）a标签的href属性内；
（3）写入到外部js文件内，并通过script标签的src属性引入文件，注意：一旦引用外部js文件，若在这个引用文件的script标签内部编写js代码，则此js代码不会被执行。

三、变量
通过关键字var来声明

四、标识符
标识符包括变量名、函数名、属性名，采用Unicode编码；
使用规则：
（1）标识符中可以含有字母、数字、下划线和"$"；
（2）标识符不能以数字开头；
（3）标识符不能是ES中的关键字；
（4）建议使用驼峰命名法命名，规则：首字母大写，每个单词的开头字母大写，其他字母小写；

五、数据类型
包括6种数据类型：String（字符串）、Number（数值）、Boolean（布尔值）、Null（空值）、Undefined（未定义）、Object（对象）；
可使用typeof来检查数据的数据类型，语法：typeof 变量名;
String（字符串）：
（1）字符串内容使用单引号或双引号引用；
（2）同种嵌套使用同种引号；
（3）转义字符"\"，例如："\n"(换行符)、"\t"(制表符);

Number（数字类型）：
（1）Number类型的数值若超过JS规定的最大值（可用Number.MAX_VALUE求得），则会返回"Infinity"(正无穷大)，使用typeof检查数据类型时仍会返回number；
（2）Number类型的数值若超过JS规定的最小值（可用Number.MIN_VALUE求得），则会返回"-Infinity"(大于0的无穷小)，使用typeof检查数据类型时仍会返回number；
（3）当使用typeof检查Number数据的数据类型时，会返回number；
（4）当数据为NaN时，NaN是一个特殊的数字，表示"Not A Number"，当使用typeof检查数据类型时，仍会返回number；
（5）JS使用浮点数运算会得到不精确的结果，不建议再JS中进行精度较高的计算；

Boolean（布尔类型）：
包含两种值：true（真）、false（假）；

Null（空）：
仅包含一种值：null；
当使用typeof检查Null数据的数据类型时，会返回object；

Undefined（未找到/未定义）：
仅包含一种值：undefined；
当使用typeof检查Undefined数据的数据类型时，会返回undefined；

六、数据转换
在进行数据转换时，JS中只能将数据转换为String、Number、Boolean三种类型；
转换为String的两种方法：
（1）toString()函数，要点：；
&#8195;&#8195;用法：被转换的数据调用此函数，例如：a.toString();
&#8195;&#8195;调用此函数会有返回值（返回值就是转换后的值），换言之，调用此函数会产生一个新变量，例如：var b=a.toString()；
&#8195;&#8195;调用函数不会影响原来的变量；
&#8195;&#8195;局限性：不能转换Null类型和Undefined类型的数据；
（2）String()函数，要点：
&#8195;&#8195;用法：将被转换的数据作为函数参数传入函数中，例如String(a)；
&#8195;&#8195;调用此函数会有返回值（返回值就是转换后的值），换言之，调用此函数会产生一个新变量，例如：var b=String(a)；
&#8195;&#8195;可以转换Null类型和Undefined类型的数据；
