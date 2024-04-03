---
title: genfstab
date: 2024-04-02 03:30
tags:
  - 硬盘/fstab/genfstab
categories:
  - Linux
---

# genfstab 
生成fstab文件
```shell
genfstab -U /mnt > /mnt/etc/fstab

#修改fstab后生效
systemctl daemon-reload
```

