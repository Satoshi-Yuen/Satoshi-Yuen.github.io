---
title: Matplotlib库中的基本图标函数
date: 2020-05-26 23:11:25
tags:
- Python
- Matplotlib
---
导入Matplotlib库的pyplot：import matplotlib.pyplot as plt
以下函数都是基于pyplot，不作参数介绍，具体用法见zeal文档：
boxplot(data,notch,position)：绘制箱型图；
bar(left,height,width,bottom)：绘制条形图；
bath(width,bottom,left,height)：绘制横向条形图；
polar(thera,r)：绘制极坐标图；
pie(data,explode)：绘制饼图；
psd(x,NFTT=256,pad_to,Fs)：绘制功率谱密度图；
specgram(x,NFTT=256,pad_to,Fs)：绘制谱图;
cohere(x,y,NFTT=256,Fs)：绘制X-Y的相关性函数；
scatter(x,y)：绘制散点图（X和Y的长度需相等）；
step(x,y,where)：绘制步阶图；
hist(x,bins,normed)：绘制直方图；
contour(X,Y,Z,N)：绘制等值图；
vlines()：绘制直方图；
stem(x,y,linefmt,markerfmt)：绘制柴火图；
plot_date()：绘制数据日期；