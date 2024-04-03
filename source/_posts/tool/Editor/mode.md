---
title: Vim Mode
tags:
  - vim
categories:
  - Tool
---
# help

- 终端。vimtutor 命令
- vim 内。:help \<关键词\>或`:he <关键词>`
- 当输入 : 命令时，按 CTRL-D 可以查看可能的补全结果。按 `<TAB>` 可以使用一个补全。
- `:set all`. 查询所有设置
- `:version`. 文件信息

# mode
- insert mode
- normal mode (esc)
  - screen command
	- 字符模式。相当于`v`
	- 行模式。相当于`V`。大写；或者按两次应用该行。eg: `dd`, `yy`,`cc`
	- 块模式。相当于`<C-v>`
  - bottom command(ex command)
- visual mode
	- 字符模式。相当于`v`
	- 行模式。相当于`V`。大写；或者按两次应用该行。eg: `dd`, `yy`,`cc`
	- 块模式。相当于`<C-v>`
