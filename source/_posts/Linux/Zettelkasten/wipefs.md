---
title: wipefs
categories:
  - Linux
date: 2024-04-02 03:30
tags:
  - 硬盘/删除分区/wipefs
aliases: 
time: '2024-04-02 03:39'
---


`wipefs /dev/sda -a`

分区表是硬盘的分区信息，要删除一个硬盘的所有分区表很麻烦的，需要 fdisk 一个一个的删除，其实 dd 命令可直接清除分区信息，当然，这也是 linux 给 root 用户留下的作死方法之一。





