---
title: 网络是怎样连接的_户根勤-笔记
tags:
  - network
categories: []
---
# 端口号范围
在网络技术中，端口（Port）大致有两种意思：一是物理意义上的端口，比如，ADSL Modem、集线器、交换机、路由器用于连接其他网络设备的接口，如RJ-45端口、SC端口等等。二是逻辑意义上的端口，一般是指TCP/IP协议中的端口，端口号的范围从0到65535，比如用于浏览网页服务的80端口，用于FTP服务的21端口等等。

16 位 2 进制数，也就是 0~65535

0~1023之间的端口号保留给预定义的服务（Well-Known Ports）。例如：http使用 80 端口。我们在编写网络应用程序时，要为程序指定 1024～ 65535 之间的端口号。

# dhcp
动态主机设置协议（DHCP）是一种使网络管理员能够集中管理和自动分配 IP 网络地址的通信协议。 在IP网络中，每个连接Internet的设备都需要分配唯一的IP地址。 DHCP使网络管理员能从中心结点监控和分配IP地址。 当某台计算机移到网络中的其它位置时，能自动收到新的IP地址。

# dhcpcd
Dynamic Host Configuration Protocol Client Daemon （net-misc/dhcpcd）是**一个能够处理IPv4 和IPv6 配置的流行DHCP 客户端**。

# DNS
域名系统（英语：Domain Name System，缩写：DNS）是互联网的一项服务。 它作为将域名和IP地址相互映射的一个分布式数据库，能够使人更方便地访问互联网。 DNS使用TCP和UDP端口53。 当前，对于每一级域名长度的限制是63个字符，域名总长度则不能超过253个字符。

/etc/resolv.conf 是DNS客户机配置文件，用于设置DNS服务器的IP地址及DNS域名，还包含了主机的域名搜索顺序。我的 /etc/resolv.conf 自动填的是路由器的 IP 地址。

# 查看网卡型号
`lspci | grep Network`

