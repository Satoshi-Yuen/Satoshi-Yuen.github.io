---
title: 路由策略之Route-Policy
date: 2020-04-30 17:31:36
tags:
- 华为HCNP
---
一个路由策略工具，可以被用来执行路由过滤和用于修改路由的属性，列表像是由多个节点构成，每一个节点是一系列条件语句和执行语句的集合；
工作原理：
&#8195;执行Route-Policy时，设备从编号最小的结点开始进行路由匹配，若被匹配的对象满足所有匹配条件，则执行该结点的执行语句，不会再继续进行下一个结点的路由匹配；若被匹配的对象有一个匹配条件不满足则进行下一个结点的路由匹配，以此类推；若最后一个结点都不能匹配，则默认执行deny动作。
基础配置：
&#8195;1、创建一个Route-Policy节点
&#8195;&#8195;一个节点下可以配置if-match语句
&#8195;&#8195;节点配置命令：route-policy (route-policy-name) {permit|deny} node (node)
&#8195;&#8195;示例：route-policy hcnp permit node 10
&#8195;&#8195;（示例提醒：若设备上不存在Route-Policy hcnp，那么执行此命令后会自动创建名为hcnp的Route-Policy，同时在该Route-Policy上创建一个匹配模式为permit、编号为10的节点）<!--more-->
&#8195;2、配置if-match语句
&#8195;&#8195;常用的if-match命令：
&#8195;&#8195;&#8195;（1）匹配ACL：if-match acl {acl-number|acl-name}
&#8195;&#8195;&#8195;（2）匹配IP前缀列表：if-match ip-prefix (ip-prefix-name)
&#8195;&#8195;&#8195;（3）匹配路由的度量值：if-match metric (metric)
&#8195;&#8195;&#8195;（4）匹配路由的出接口：if-match (interface-type) (interface-number)
&#8195;&#8195;&#8195;（5）匹配路由的标记：if-match tag (tag)
&#8195;&#8195;一个节点可以包含多条if-match语句，除了if-match route-type语句和if-match interface语句是或的关系外，其他的每一条if-match语句都是并列（与）关系，在执行时，每一条if-match语句都满足时，匹配对象才是被称为匹配该节点；
&#8195;&#8195;当一个节点当中不包含任何if-match语句时，这时候的匹配对象都是匹配的。
&#8195;3、配置apply语句
&#8195;&#8195;apply命令可以对所匹配的路由的某些属性进行修改，属性包括路由的度量值（cost）、优先级值（preference）、标记（tag）等；常用的apply命令有：
&#8195;&#8195;&#8195;（1）设置路由的度量值：apply cost [+|-](cost)
&#8195;&#8195;&#8195;（2）设置路由的度量值类型：
&#8195;&#8195;&#8195;&#8195;1）设置IS-IS度量值类型：apply cost-type {external|internal}
&#8195;&#8195;&#8195;&#8195;2）设置OSPF度量值类型：apply cost-type {type1|type2}
&#8195;&#8195;&#8195;（3）设置路由下一跳地址：apply ip-address next-hop {ipv4-address|peer-address}
&#8195;&#8195;&#8195;（4）设置路由的优先级：apply preference (preference)
&#8195;&#8195;&#8195;（5）设置路由的标记：apply tag (tag)
&#8195;&#8195;一个节点可以不包含任何apply语句，这时就只进行路由过滤而不进行路由属性值的修改。