---
title: process manager
categories: Linux
tags: linux
---
`top`
`ps -ef|grep`
`free -h`
htop 比 top 更好
pstree

# 服务/守护进程

## service 命令

计算机中，一个正在执行的程序或命令，被叫做“进程”(process)
启动之后一直存在、常驻内存的进程，一般被称作“服务”(service) 或守护进程 (daemon)

基本语法

```shell
service 服务名 start|stop|restart|status
```

查看服务的方法:  /etc/init.d/服务名

## systemd

基本语法

```shell
systemctl start|stop|restart|status|enable|disable 服务名
```

查看服务的方法：/usr/lib/systemd/system

# 系统运行级别







