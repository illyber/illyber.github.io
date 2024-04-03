---
title: Vim Plugin
tags:
  - vim
categories:
  - Tool
---
# plug-in
## preservim/nerdcommente

[主页](https://github.com/preservim/nerdcommenter#usage)

`:help nerdcommenter`

- `[count]<leader>cc` **|NERDCommenterComment|**

Comment out the current line or text selected in visual mode.

- `[count]<leader>c<space>` **|NERDCommenterToggle|**

  Toggles the comment state of the selected line(s). If the topmost selected line is commented, all selected lines are uncommented and vice versa.

- `[count]<leader>ci` **|NERDCommenterInvert|**

  Toggles the comment state of the selected line(s) individually.

# 插件

```bash
# 安装插件
git clone https://github.com/junegunn/vim-plug
cp ./vim-plug/plug.vim  ~/.vim/autoload/plug.vim
在 vim 内运行 ex 命令
:PlugInstall
:PlugUpdate

# 卸载插件
:PlugClean

```

