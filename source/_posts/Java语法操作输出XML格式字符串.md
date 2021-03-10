---
title: Java语法操作输出XML格式字符串
date: 2021-03-09 16:48:33
tags:
- Java
- XML
---

以下是基于dom4j生成XML格式的操作，实现思路源于网络

### 1、导入需要的类

````java
import org.dom4j.Document;
import org.dom4j.DocumentHelper;
import org.dom4j.Element;
import org.dom4j.io.OutputFormat;
import org.dom4j.io.XMLWriter;
````

### 2、XML格式结构构建

````xml
//创建文档，相当于是新建了一个文档
Document doc = DocumentHelper.createDocument();
//创建根元素
Element root = doc.addElement("root");
//创建父元素
Element hrmlist = root.addElement("hrmlist");
//创建子元素
Element hrm = hrmlist.addElement("hrm");
//子元素插入标签和相应值
hrm.addAttribute("action","add");
````

### 3、插入标签与内容

````xml
//构建一对名为workcode的标签，例如：<workcode></workcode>
Element workcode = hrm.addElement("workcode");
//在这一对标签中插入内容，例如：<workcode>psncode</workcode>
workcode.setText(psncode);
````

若想在同一个父标签下构建多对标签，按上述方式即可

### 4、内容格式化为XML

````xml
//定义字符数组输出流
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
//定义输出的格式
OutputFormat format = OutputFormat.createPrettyPrint();
format.setIndent("    ");  //设置缩进
//定义XML格式的writer
XMLWriter writer = new XMLWriter(outputStream, format);
//从根结点输出整一个XML格式内容
Document document = root.getDocument();
writer.write(document);
strResult = new String(outputStream.toByteArray(), "utf-8");
````

最后的strResult则是整一个xml格式内容的字符串。



以上