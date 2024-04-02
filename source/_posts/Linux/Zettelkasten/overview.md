---
title: overview
categories:
  - Linux
date: 2024-04-02 05:20
tags:
  - linux-set/概览
---

---
# 设置 `meta` 键为 overview 快捷键：
```shell
kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta "org.kde.kglobalaccel,/component/kwin,,invokeShortcut,Overview"
```
reload your KWin settings without restarting KWin by running:
```shell
qdbus org.kde.KWin /KWin reconfigure
```




---
