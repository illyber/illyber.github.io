---
title: process-manager
date: 2024-04-02 03:30
tags: 
categories:
  - Linux
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

# 锁屏后继续执行命令

详见：[在后台运行 Linux 命令的方法](https://bambrow.com/20210617-run-linux-command-background/#%E5%9C%A8%E5%90%8E%E5%8F%B0%E8%BF%90%E8%A1%8CLinux%E5%91%BD%E4%BB%A4)

相关概念：

- 后台进程是指在终端运行的程序或脚本，它在后台运行而不会占据终端窗口。后台进程可以继续运行，即使终端窗口被关闭或用户注销。

- 前台进程是指在终端运行的程序或脚本，它会占据终端窗口并与用户进行交互。前台进程通常会受到终端窗口的状态变化的影响，比如锁屏或终端窗口关闭。

即使锁屏后脚本原本是前台进程，它也会成为后台进程继续运行。

虽然后台进程的脚本可以在锁屏后继续运行，但是前台进程的脚本可能会被挂起或中断。当系统锁屏时，它会暂停前台进程并将其置于休眠状态。如果你的脚本是前台进程，它在锁屏后可能会被暂停。

有一种情况下，前台进程的脚本可能会继续运行。如果你在锁屏前使用了`tmux`或`screen`等终端多路复用工具，并在其中运行了脚本，那么在锁屏后，这些工具会继续运行，脚本也会继续在这些工具中运行。







