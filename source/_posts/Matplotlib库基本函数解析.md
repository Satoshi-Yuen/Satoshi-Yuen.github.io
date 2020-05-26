---
title: Matplotlib库基本函数解析
date: 2020-05-26 17:16:47
tags:
- Python
- Matplotlib
---
Matplotlib库：绘制各种类可视化图形的命令子库。
查看Matplotlib库效果图网址：http://matplotlib.org/gallery.html
导入Matplotlib库：import matplotlib.pyplot as plt
基本函数及解析：
plot(x,y,format_String,kargs)：设置坐标轴的x、y的取值，参数解析：
&#8195;x：表示x轴方向的列表或数组的坐标值，可选项；
&#8195;&#8195;&#8195;注意：当在一个坐标轴内绘制多条曲线时，x为必选项；
&#8195;y：表示y轴方向的列表或数组的坐标值，必选项；
&#8195;&#8195;&#8195;注意：只填写一个数组或列表时，数组或列表数据默认为坐标轴y轴的数据，x轴的坐标根据数据的索引自动生成；
&#8195;format_String：控制曲线的格式字符串；由颜色字符、线体样式和标记字符构成；
&#8195;注意：颜色字符、线体样式和标记字符要写在同一对''中，每一种样式不需要字符隔开；
&#8195;例子：'b-.'；
&#8195;kargs：表示有多组(x,y,format_String)；

savefig('文件名',dpi)：将输出图像存储为文件，文件类型默认为PNG；
&#8195;注意：可通过dpi修改文件输出的质量且dpi为可选项；
&#8195;例子：plt.savefig('wenjian',dpi=700)；

axis()：设置对坐标轴的刻度；
&#8195;例子：plt.axis([0,10,0,5])，例子解析："0,10"表示x轴范围为0-10，"0,5"表示y轴范围为0-5；

subplot(nrows,ncols,plot_number)：在全局绘图中进行分区并定位，参数解析：
&#8195;nrows：划分的区域的总行数；
&#8195;ncols：划分的区域的总列数；
&#8195;plot_number：定位的区域号；

pyplot中显示中文的方式：
先介绍在x、y轴方向设置文字的函数
xlabel()：在x轴上设置文字；
ylabel()：在y轴上设置文字；
&#8195;栗子：xlabel("文字内容")
正题：
（1）rcParams:设置文字在图像中的体现；
&#8195;可选参数：
&#8195;&#8195;font-family：设置中文字体；
&#8195;&#8195;font-style：设置字体样式，可选值：normal（正常）、italic（斜体）；
&#8195;&#8195;font-size：设置字体大小；
&#8195;使用语法栗子：matplotlib.rcParams['font-family']="字体样式"；
&#8195;注意：rcParams需要和xlabel或ylabel（不带fontproperties）结合使用；
（2）使用fontproperties属性：
在有文字输出的函数，加上一个fontproperties属性，这个属性是用来设置字体的，使用fontproperties属性就不需要使用rcParams()；
&#8195;栗子：xlabel("字体内容",fontproperties='字体样式')；

title()：对图像整体增加文本标签（题目）；

text()：在任意位置增加文本；

annotate(s,xy,xytext=crd,arrowprops=dict)：在图形中增加带箭头的注解；
&#8195;参数解析：
&#8195;&#8195;（1）s：注解内容；
&#8195;&#8195;（2）xy：箭头所指的注解位置，填写一对坐标；
&#8195;&#8195;（3）xytext=crd：注解显示的开始位置；
&#8195;&#8195;（4）arrowprops=dict：社会箭头样式；
&#8195;例子：annotate("注解内容",(1,1),xytext=(2,2),arrowsprops=dict(facecolor="white",shrink=0.5,width=2))

plot子绘图区域：
subplot2grid(gridspec,curspec,colspan,rowspan)：自定义划分复杂的网格区域并定位；
&#8195;参数解析：
&#8195;&#8195;（1）gridspec：划分初始网格，例如：划分为3x3网格：(3,3)
&#8195;&#8195;（2）curspec：选中网格，例如：选中第2行第1个：(1,0)
&#8195;&#8195;（3）colspan：y轴方向合并列，可选值，例子：colspan=3；
&#8195;&#8195;（4）rowspan：x轴方向合并行，可选值，例子：rowspan=2；
