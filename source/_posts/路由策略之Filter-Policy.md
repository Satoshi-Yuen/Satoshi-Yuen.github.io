---
title: 路由策略之Filter-Policy
date: 2020-04-30 17:32:20
tags:
- 华为HCNP
---
一种路由过滤器，只能对路由信息进行过滤而不能过滤数据包，可应用在RIP、OSPF、IS-IS以及BGP等；
Filter-Policy对RIP发送/接收的路由进行过滤
&#8195;ACL：
&#8195;&#8195;发送的配置命令：filter-policy (acl-number) export 接口/协议 （export表示出方向）；
&#8195;&#8195;接收的配置命令：filter-policy (acl-number) import 接口 （import表示入方向）；
IP前缀列表：
&#8195;&#8195;发送的配置命令：filter-policy ip-prefix (列表名) export 接口/协议 （export表示出方向）；
&#8195;&#8195;接收的配置命令：filter-policy ip-prefix (列表名) import 接口 （import表示入方向）；<!--more-->
Filter-Policy对向其他协议发布/接收的路由进行过滤
&#8195;ACL：
&#8195;&#8195;发布的配置命令：filter-policy (acl-number) export 协议名/接口
（此配置命令的意思是：在路由器通过Filter-Policy过滤的路由加入到路由表后，路由器就不会发送关于被过滤掉的的路由，从而路由器无法发布被过滤的路由到OSPF中，使得其他路由器不会学习到被过滤掉的路由）
&#8195;&#8195;接收的配置命令：filter-policy (acl-number) import 协议名/接口
&#8195;IP前缀列表：
&#8195;&#8195;发布的配置命令：filter-policy ip-prefix (列表名) export 协议名/接口
&#8195;&#8195;接收的配置命令：filter-policy ip-prefix (列表名) import 协议名/接口