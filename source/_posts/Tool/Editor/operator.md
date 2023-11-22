---
title: Vim Operator
tags:
  - vim
categories:
  - Tool
  - Editor
---
The motion commands can be used after an operator command, to have the command operate on the text that was moved over.  That is the text between the cursor position before and after the motion.  Operators are generally used to delete or change text.
# 通用
`{number}d`
`d{motion}`
`d{object}`
`"[x]d{motion}`
`dd` 行模式/linewise
`d` 及物动词，`x` 不及物动词.

# 剪切并修改
- `cc`。删除该行并插入. 重复一次是可视化的行模式 `V`
- `s`。删除该字符并插入，是`c`的快捷键
- vim里`y`，`d`，`x`，`c`复制
- `A`. 在行末追加

# 删除剪切复制粘贴
- `dvb`. 位于单词末尾时删除这个单词。
- `daw`. 删除光标所在单词
- paste contents copied from `y$` to new line
- `viwp`. 用剪贴板替换选定的内容。
- `:%s/^.\{10\}//`。删除每行开始十个字符。
- `:%s/.\{10\}$//`。删除每行最后十个字符。

```
:[line]pu[t] [x]    Put the text [from register x] after [line] (default
                    current line).  This always works |linewise|, thus
                    this command can be used to put a yanked block as
                    new lines.

:[line]pu[t]! [x]   Put the text [from register x] before [line]
                    (default current line).
```

- `-7 co +10`. 相对位置不用jk，上-下+，将上面第七行复制到下面第十行。可以把-7换成范围-10,-5
- `"-yy`, 将当前行复制到寄存器`"-`

# 插入/追加
- `:r file2`. 在 file1 的光标位置追加 file2 的内容

- 在多个行首/行位插入
  - 1: 定位光标
    2: CTRL+v #进入Visual Mode。
    3: j #选择要在哪些行加入？！
    4: I #一定是大写！
    5: 输入要插入的文本
    6: 按`esc`后完成插入

行首 `:%s/^/your_word/`
行尾 `:%s/$/your_word/`
- 在本行行首插入：`I`
- 在下一行行首插入：`I`
- 在本行行尾添加：`A`

# replacement mode
- `r` 替换当前字符，不会进入 insert mode
- `R` 替换整行，不会进入 insert mode
- `c` cut. 与 `d` 类似，可以跟 motion，但是会进入 insert mode，并且 `cw` 时不会删除空格
- `C` 或 `cc` 删除整行（行模式）并进入 insert mode
- `s` 同`cl`, 删除当前字符并进入 insert mode
- `S` synonym of `cc`, 删除当前行并进入 insert mode

但前都可以跟数字。所有normal command前都可以跟数字，重复执行多少次。

# 缩进
## 缩进调整
缩进调整的帮助查找命令： :help shift-left-right，或者直接help下面缩进调整的任意一个命令。缩进调整操作的执行与vim中的shiftwidth参数的值有关系， 在前文的vimrc配置文件中，已经将shiftwidth设置为4，表示每一次缩进的宽度均为4个空格长，可以参照进行修改。

以下为常用的缩进快捷操作和命令：

- 当前行向右缩进一次：操作 ? 或者输入命令 :>
- 当前行向左缩进一次：操作 ? 或者输入命令 :<
- 从第m行起，到第n行止向右缩进一次： 输入命令 :m,n> 等价于命令 :m>(n-m+1)
- 从第m行起，到第n行止向左缩进一次： 输入命令 :m,n< 等价于命令 :m<(n-m+1)
- 从第m行起共n行向右缩进一次： 输入命令 :m>n 等价于命令 :m,m+n-1>
- 从第m行起共n行向左缩进一次： 输入命令 :m

# 折叠
[VIM中文用户手册:折叠](https://yianwillis.github.io/vimcdoc/doc/usr_28.html#usr_28.txt)

[vim折叠快捷键](https://www.cnblogs.com/zlcxbb/p/6442092.html)

```vimscript
"full form of fdm is foldmethod
"按语法折叠
set fdm=syntax
```

`zc`, `zo`, `zk`, `zj`, `zr`, `zm`
- `zR`, 展开所有折叠

- 离开时自动保存折叠情况，打开文档时自动载入折叠情况

```vimscript
au BufWinLeave * silent mkview
au BufWinEnter * silent loadview
```

# 合并
`<S+j>`. 合并当前行和下一行

# 撤销/取消撤销
- `u`, 撤销；`<c-r>`, 取消撤销