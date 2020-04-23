---
title: BGP--基础配置命令及解析（持续更新）
date: 2020-04-16 17:12:15
tags:
- 华为HCNP
- BGP
---
bgp (as-number)：创建BGP进程；
router-id：在BGP进程下指定用于该进程的路由器ID；
peer (peer-address) as-number (as-number)：配置一个BGP对等体并指定该对等体所处的AS；
display bgp peer：查看该设备所指定的BGP对等体；
display bgp routing-table：查看设备的BGP路由表；关于路由表中的一些符号解析：
&#8195;&#8727;：表示路由有效；
&#8195;&#62;：表示最优路由；
&#8195;i：表示此路由是从IBGP对等体学习到的，Origin为IGP（从EBGP中学习到的没有i标志）；
&#8195;?：表示Origin为Incomplete<!--more-->
import-route：可以将路由发布到BGP，例如，在BGP路由器下，import-route ospf 1可以将ospf的路由发布到BGP（只能IGP到BGP，不可逆）；
next-hop-local：修改路由的下一跳（在通告路由的路由器上配置）；
peer (Loopback-IP) connect-interface (Loopback)：用于指定本设备使用Loopback接口和具有环回口路由器建立BGP对等体关系；
peer (对等体IP) ebgp-max-hop (最大跳数)：配置BGP允许与非直连的设备建立EBGP对等体关系，同时可以设置所允许的最大跳数（该跳数影响BGP报文的TTL值），当BGP使用loopback接口建立EBGP对等体关系时，必须配置这条命令，并且跳数必须大于等于2，否则EBGP对等关系无法建立。
