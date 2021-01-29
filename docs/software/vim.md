# Vim

## Mode of Vim

* Normal mode  `[ESC]<default>`
* Insert mode  `[iI aA oO]`
* Visual mode  `[v]`
* Command-line mode `[:]`
* Ex mode `[Q]`

除`Ex`模式需输入`visual`退出外,其它任何模式都可以通过按下两次`ESC`键返回至`Normal`模式。

## Common cmds

### basic

* `u` : 撤销上一次修改操作
* `<Ctrl-R>` : 重做上一次撤销的修改
* `.` : 重复上一次修改操作
* `:q` : 未修改内容的情况下退出
* `:q!` : 强制退出，已修改部分不生效
* `:w` : 保存修改内容
* `:wq` : 保存文件并退出
* `:wq!` : 强制保存文件并退出

### insert

* `i` : 在光标前插入
* `I` : 在行首插入
* `a` : 在光标后插入
* `A` : 在行尾插入
* `o` : 向下插入一行
* `O` : 向上插入一行
* `s` : 删除当前字符并插入
* `cc` : 删除当前行并插入
* `ch` : 删除前一个字符并插入
* `cw` : 删除当前单词并插入

### delete

* `dd` : 删除当前行
* `dw` : 删除当前所在的单词
* `d$` : 删除当前位置到行末的所有字符
* `d0` : 删除当前位置到行首的所有字符
* `d^` : 删除当前位置到当前行首个非空字符的所有字符
* `x`  : 删除当前单个字符
* `ndd` : 删除包括当前行往后的n行内容，n=1,2,3...，如: 4dd
* `ndw` : 删除包括当前单词往后的n个单词，n=1,2,3...，如: 4dw
* `nd$` : 删除当前位置到往后n行末尾的所有内容，n=1,2,3...，如: 4d$
* `nx`  : 删除包括当前字符往后的n个字符，n=1,2,3...，如: 4x

!!! tip "说明"
    下文中的 `n` 除非特殊说明，否则均代表数字(n=1,2,3,...)

### copy

* `yy`  :复制当前行
* `yw`  :复制当前所在的单词
* `y$`  :复制当前位置到行末的所有字符
* `y0`  :复制当前位置到行首的所有字符
* `y^`  :复制当前位置到当前行首个非空字符的所有字符
* `nyy` :复制包括当前行往后的n行内容，n=1,2,3...，如: 4yy
* `nyw` :复制包括当前单词往后的n个单词，n=1,2,3...，如: 4yw
* `ny$` :复制当前位置到往后n行末尾的所有内容，n=1,2,3...，如: 4y$

### paste

* `p` : 粘贴到当前位置后面或下一行
* `P` : 粘贴到当前位置前面或上一行
* `np` : 向后复制n次
* `nP` : 向前复制n次

### find/replace

* `/<PATTERN>` : 向下查找首个匹配项
* `?<PATTERN>` : 向上查找首个匹配项
* `n` : 向下查找匹配项
* `N` : 向上查找匹配项
* `*` : 向上查找与光标所在单词相同的单词
* `R` : 进入替换模式

### jump

* `h` : 左移一个字符
* `j` : 下移一行
* `k` : 上移一行
* `l` : 右移一个字符
* `gj` : 下移一个逻辑行
* `gk` : 上移一个逻辑行
* `gg` : 跳至首行
* `G` : 跳至尾行
* `w` : 跳至下一个单词的首字符
* `b` : 跳至上一个单词的首字符
* `e` : 跳至下一个单词的尾字符
* `ge` : 跳至上一个单词的尾字符
* `0` : 跳至当前行首个字符
* `^` : 跳至当前行首个非空字符
* `$` : 跳至当前行末尾
* `nG` : 跳至第n行
* `:n` : 跳至第n行

!!! tip "说明"
    在 `vim` 中，存在 **逻辑行** 和 **物理行** 两个概念，**物理行** 指的是 `:set number` 后显示行号对应的行，**逻辑行** 是单行显示不了后自动回绕自下一行产生的。

``` vim
1 test information;
2 test information;test information;<tag21>test information;test information;
  test information;test information;<tag22>test information;
3 test information;test information;<tag31>test information;test information;
  test information;test information;<tag32>test information;test information;
  test information;test information;<tag33>test information;
4 test information;test information;<tag41>
5
6 test information;
```

上面显示的第2,3行由于单行无法显示完整内容所以回绕至下一行，逻辑行是包括所有回绕行的，而物理行是按左侧编号对应的行进行操作的。

若当前光标在`<tag21>`的位置，那么物理行操作`j`将会把光标移至`<tag31>`，继续`j`会移至`<tag41>`；但若是换成逻辑行操作`gj`，则会将光标移至`<tag22>`，连续执行5次才会移至`<tag41>`。这些就是逻辑行与物理行的区别了。

## Window cmds

### open multi-window

* `vi -o file1 file2` : 打开两个纵向分隔的窗口
* `vi -O file1 file2` : 打开两个横向分隔的窗口
* `vi -o4` : 打开4个纵向分隔的窗口
* `vi -O4` : 打开4个横向分隔的窗口

### edit multi-window

* `:sp file`: 在当前窗口下方打开新的窗口
* `:vsp file`: 在当前窗口右侧打开新的窗口
* `ctrl w s`: 在当前窗口下方打开新的窗口，打开当前窗口副本
* `ctrl w v`: 在当前窗口右侧打开新的窗口，打开当前窗口副本

!!! tip
    当 `sp` `vsp` 不指定文件时，默认打开当前所在窗口文件的副本

### romaing

* `ctrl w h`: 切到左侧窗口
* `ctrl w j`: 切到下测窗口
* `ctrl w k`: 切到上测窗口
* `ctrl w l`: 切到右侧窗口
* `ctrl w w`: 循环切换窗口，从上到下，从左到右
* `ctrl w p`: 切到上一次访问的窗口
* `ctrl w t`: 切到最左上角的窗口
* `ctrl w b`: 切到最右下角的窗口

### layout

改变窗口布局

* `ctrl w H`: 移动窗口至屏幕左侧，占用全部高度
* `ctrl w J`: 移动窗口至屏幕底部，占用全部宽度
* `ctrl w K`: 移动窗口至屏幕顶部，占用全部宽度
* `ctrl w L`: 移动窗口至屏幕右侧，占用全部高度
* `ctrl w T`: 移动窗口至新的分页，之后可通过 `gf` 切换分页
* `ctrl w r`: 向右或向下交换窗口
* `ctrl w R`: 向右或向下交换窗口
* `ctrl w x`: 交换同列或同行窗口位置

### resize

* `ctrl w =`: 平均分布窗口大小
* `ctrl w |`: 单独占用整个屏幕
* `ctrl w -`: 当前窗口高度减少一行
* `ctrl w +`: 当前窗口高度增加一行
* `ctrl w >`: 当前窗口宽度减少一列
* `ctrl w <`: 当前窗口宽度增加一列

## useful cmds

* `:g/pattern/d`: 删除全局匹配行
* `:%s/pattern/replace/g`: 全局替换匹配项, `gc` 可以单独控制每个匹配项

## edit binary

编辑二进制文件

1. 使用 `vi -b file` 打开文件
2. 命令模式 `:%!xxd` 让文件以16进制形式与ASCII形式显示，类似于`hexdump -C`
3. 编辑文件结束后，设置 `:%!xxd -r`

## add line number

添加当前行行号

```vim
:%s/^/\=line('.')/
```

添加所选行行号，`'<`代表所选行首行，`'>`代表所选行尾行

```vim
:'<,'>s/^/\=(line('.')-line("'<")+1).'. '/
```

其它方法

1. `:%!cat -n`
2. `:'<,'>!cat -n`
3. `%!nl`
