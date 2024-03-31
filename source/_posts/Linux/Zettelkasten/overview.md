2024 0331 16:25
Tags: #linux-set/概览

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
