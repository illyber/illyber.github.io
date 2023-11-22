---
title: kde plasma
categories:
  - Linux
tags:
  - linux
---
# application launcher
修改位于 `/usr/share/applications`  的 desktop entry，就能让应用出现在启动器菜单，链接可以放到桌面。
# 设置 `meta` 键为 overview 快捷键：
```shell
kwriteconfig5 --file kwinrc --group ModifierOnlyShortcuts --key Meta "org.kde.kglobalaccel,/component/kwin,,invokeShortcut,Overview"
```
reload your KWin settings without restarting KWin by running:
```shell
qdbus org.kde.KWin /KWin reconfigure
```