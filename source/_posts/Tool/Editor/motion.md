---
title: vim Motion
tags:
  - vim
categories:
  - Tool
  - Editor
---
- linewise 就是影响整行的。linewise motion 的操作与光标起始、结束位置的横坐标无关，只与纵坐标有关。举例：j 、k。比如指令 dj 会删掉当前整行及下面的整行，无论光标的横坐标是在行中还是哪里。
- characterwise 就是影响光标移动中间部分的。characterwise motion 的操作与光标的起始、结束位置的横坐标有关。举例：w、W、e、E 等等。比如指令 dw 会删除一个词，即使这个 w 的 motion 跨行移动了，也只是删除起始和结束所包含的中间这个单词的部分，不会影响整行。
- exclusive 不包含结束位置。比如 w 会移动下个单词的首字母，但是使用 dw 时下个单词的首字母不会被删除。
- inclusive 包含结束位置。比如 t{char}、f{char} 等等。比如 fc 会把光标移动到离光标最近的下一个 c 字母上，而 dfc 会把光标结束时所在位置的 c 字母也会删掉。
- exclusive-linewise 跨行但不包含结束的那行。比如 d} 不会删除光标移动结束所在的行，但之前的行会删掉。相当于 linewise，但保留结束行。

参考：[知乎用户](https://www.zhihu.com/question/548901776/answer/2637739765)

![img](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307011656374.png)
参考：[心止在焉 - motion in vim](https://zoub.in/engineering/docs/updates/2015/motion-in-vim.html)

翻页

| effect                              | command                     |
| ----------------------------------- | --------------------------- |
| 向下翻页 (forward)                  | <kbd>ctrl</kbd><kbd>f</kbd> |
| 向上翻页 (backward)                 | <kbd>ctrl</kbd><kbd>b</kbd> |
| 向下翻半页 (down)（映射成`<Down>`） | <kbd>ctrl</kbd><kbd>d</kbd> |
| 向上翻半页 (up)（映射成`<Up>`）     | <kbd>ctrl</kbd><kbd>u</kbd> |

单词移动

| effect                              | command                     |
| ----------------------------------- | --------------------------- |
| to the beginning of the next word   | <kbd>w</kbd>                |
| to the beginning of the last word   | <kbd>b</kbd>                |
| to the end of the next word         | <kbd>e</kbd>                |
| to the end of the last word         | <kbd>g</kbd> <kbd>e</kbd>   |

行搜索

| effect                  | command      |
| ----------------------- | ------------ |
| search in the line      | <kbd>f</kbd> |
| back search in the line | <kbd>F</kbd> |
| 跳到光标后第三个 a      | `3fa`        | 

`, ;`在输入上述命令后，可以使用分号和逗号正向或反向重复前面的命令

