---
title: Vim 中的按键标识符
tags:
  - vim
categories:
  - Tool
---
# vim键位图
![vi-vim-cheat-sheet-sch](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202301281946924.gif)

# vim中的按键标识符
```vimscript
					*key-notation* *key-codes* *keycodes*
下面这些按键的名称文档里会用到。它们也可以用在 ":map" 命令里 (按下 CTRL-K 再按
下你想输入的键就可以输入该键的键名)。

标识符		含义			等价于	十进制数值	~
-----------------------------------------------------------------------
<Nul>		零			CTRL-@	  0 (存储为 10) *<Nul>*
<BS>		退格键			CTRL-H	  8	*backspace*
<Tab>		制表符			CTRL-I	  9	*tab* *Tab*
							*linefeed*
<NL>		换行符			CTRL-J	 10 (用作 <Nul>)
<FF>		换页符			CTRL-L	 12	*formfeed*
<CR>		回车符			CTRL-M	 13	*carriage-return*
<Return>	同 <CR>					*<Return>*
<Enter>		同 <CR>					*<Enter>*
<Esc>		转义			CTRL-[	 27	*escape* *<Esc>*
<Space>		空格				 32	*space*
<lt>		小于号			<	 60	*<lt>*
<Bslash>	反斜杠			\	 92	*backslash* *<Bslash>*
<Bar>		竖杠			|	124	*<Bar>*
<Del>		删除				127
<CSI>		命令序列引入		ALT-Esc	155	*<CSI>*
<xCSI>		图形界面的 CSI				*<xCSI>*

<EOL>		行尾 (可以是 <CR>、<NL> 或 <CR><NL>，
		根据不同的系统和 'fileformat' 而定)	*<EOL>*

<Up>		光标上移键			*cursor-up* *cursor_up*
<Down>		光标下移键			*cursor-down* *cursor_down*
<Left>		光标左移键			*cursor-left* *cursor_left*
<Right>		光标右移键			*cursor-right* *cursor_right*
<S-Up>		Shift＋光标上移键
<S-Down>	Shift＋光标下移键
<S-Left>	Shift＋光标左移键
<S-Right>	Shift＋光标右移键
<C-Left>	Control＋光标左移键
<C-Right>	Control＋光标右移键
<F1> - <F12>	功能键 1 到 12			*function_key* *function-key*
<S-F1> - <S-F12> Shift＋功能键 1 到 12		*<S-F1>*
<Help>		帮助键
<Undo>		撤销键
<Insert>	Insert 键
<Home>		Home				*home*
<End>		End				*end*
<PageUp>	Page-up				*page_up* *page-up*
<PageDown>	Page-down			*page_down* *page-down*
<kHome>		小键盘 Home (左上)		*keypad-home*
<kEnd>		小键盘 End (左下)		*keypad-end*
<kPageUp>	小键盘 Page-up (右上)		*keypad-page-up*
<kPageDown>	小键盘 Page-down (右下)		*keypad-page-down*
<kPlus>		小键盘 +			*keypad-plus*
<kMinus>	小键盘 -			*keypad-minus*
<kMultiply>	小键盘 *			*keypad-multiply*
<kDivide>	小键盘 /			*keypad-divide*
<kEnter>	小键盘 Enter			*keypad-enter*
<kPoint>	小键盘 小数点			*keypad-point*
<k0> - <k9>	小键盘 0 到 9			*keypad-0* *keypad-9*
<S-...>		Shift＋键			*shift* *<S-*
<C-...>		Control＋键			*control* *ctrl* *<C-*
<M-...>		Alt＋键 或 Meta＋键		*meta* *alt* *<M-*
<A-...>		同 <M-...>			*<A-*
<D-...>		Command＋键 (只用于 Macintosh)	*<D-*
<t_xx>		termcap 里的 "xx" 项目对应的键
-----------------------------------------------------------------------

备注: Shift＋方向键，帮助键和撤销键只在少数终端里有效。在 Amiga 机器上，Shift
＋功能键 10 生成命令序列引入码 (CSI)，也用于键序列。只有再按一个键，该代码才能
被识别出来。

备注: Delete 键有两个键码。一般是十进制的 ASCII 码 127，这个总能认出来。但有些
delete 键会发送 termcap 项 "kD" 的值。这两个值有同样的效果。另见 |:fixdel|。

备注: 小键盘上的按键与其对应的 "正常" 按键一样。例如，<kHome> 与 <Home> 有同样
的效果。如果小键盘上的键发送的原始键码与 "正常" 键相同，那么将被认为是按下了
"正常" 键。例如，如果 <kHome> 发送的键码与 <Home> 相同，当按下 <khome> 的时
候，Vim 会认为你按下了 <Home>。<kHome> 的映射此时不会有效。

								*<>*
例子中经常使用 <> 记法。有时这只是用来说明你需要输入什么，但经常它需要照本义键
入，例如在 ":map" 命令里。规则是:
 1.  任何可显示的字符都可以直接键入，反斜杠和 '<' 除外。
 2.  反斜杠用两个反斜杠表示 "\\"，或者用 "<Bslash>"。
 3.  真正的 '<' 用 "\<" 或 "<lt>" 表示。只有在没有歧义的时候才可以直接用 '<'
     表示。
 4.  "<key>" 的意思是特殊键。其含义上面的表格都有介绍，下面是一些例子:
	   <Esc>		Escape 键
	   <C-G>		CTRL-G
	   <Up>			光标上移键
	   <C-LeftMouse>	Control＋鼠标左键点击
	   <S-F11>		Shift＋功能键 11
	   <M-a>		Meta- a (第 8 位置位的 'a')
	   <M-A>		Meta- A (第 8 位置位的 'A')
	   <t_kd>		termcap 的 "kd" 项 (光标下移键)
    尽管你可以指定 {char} 为多字节字符的 <M-{char}>，Vim 可能不知道那对应什么
    字节序列，所以不能工作。

如果你想在 Vim 里使用 <> 的完整记法，必须确定 'cpoptions' 里不包括 '<' 标志位
(如果没有置位 'compatible'，默认值就是这样)。 >
	:set cpo-=<
这里，<> 记法使用 <lt> 来抵消键名的特殊含义。使用反斜杠也可以，但是需要去掉
'cpoptions' 里的 'B' 标志位。

下面的例子是把 CTRL-H 映射成六个字符 "<Home>":
	:imap <C-H> \<Home>
	:imap <C-H> <lt>Home>
第一种方法只有在 'cpoptions' 里没有 'B' 标志位才好用。第二种总成立。
要在映射中得到按本义出现的 "<lt>" 这几个字符: >
	:map <c-l> <lt>lt>

对于映射，缩写和菜单命令你可以用复制-粘贴直接使用手册里的例子。你也可以手动键
入它们，包括 '<' 和 '>'。但是在其它命令里，比如 ":set" 和 "autocmd"，这是_不_
行的！
==============================================================================
```
