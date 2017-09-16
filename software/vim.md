## Mode of Vim

* Normal mode  `[ESC]<default>`
* Insert mode  `[iI aA oO]`
* Visual mode  `[v]`
* Command-line mode `[:]`
* Ex mode `[Q]`

除`Ex`模式需输入`visual`退出外,其它任何模式都可以通过按下两次`ESC`键返回至`Normal`模式。

## Common cmds

### basic

| 指令 | 说明 |
| :--: | :--- |
| `u` | 撤销上一次修改操作 |
| `<Ctrl-R>` | 重做上一次撤销的修改 |
| `.` | 重复上一次修改操作 |
| `:q` | 未修改内容的情况下退出 |
| `:q!` | 强制退出，已修改部分不生效 |
| `:w` | 保存修改内容 |
| `:wq` | 保存文件并退出 |
| `:wq!` | 强制保存文件并退出 |

### delete

| 指令 | 说明 |
| :---: |:---|
| `dd` | 删除当前行 |
| `dw` | 删除当前所在的单词 |
| `d$` | 删除当前位置到行末的所有字符 |
| `d0` | 删除当前位置到行首的所有字符 |
| `d^` | 删除当前位置到当前行首个非空字符的所有字符 |
| `x`  | 删除当前单个字符 |
| `ndd` | 删除包括当前行往后的n行内容，n=1,2,3...，如: 4dd |
| `ndw` | 删除包括当前单词往后的n个单词，n=1,2,3...，如: 4dw |
| `nd$` | 删除当前位置到往后n行末尾的所有内容，n=1,2,3...，如: 4d$ |
| `nx`  | 删除包括当前字符往后的n个字符，n=1,2,3...，如: 4x |

**说明：**下文中的`n`除非特殊说明，否则均代表数字(n=1,2,3,...)

### copy

`copy`的指令与`delete`格式完全一致，只是将`d`改成了`y`。

| 指令 | 说明 |
| :---: |:---|
| `yy`  |复制当前行 |
| `yw`  |复制当前所在的单词 |
| `y$`  |复制当前位置到行末的所有字符 |
| `y0`  |复制当前位置到行首的所有字符 |
| `y^`  |复制当前位置到当前行首个非空字符的所有字符 |
| `nyy` |复制包括当前行往后的n行内容，n=1,2,3...，如: 4yy |
| `nyw` |复制包括当前单词往后的n个单词，n=1,2,3...，如: 4yw |
| `ny$` |复制当前位置到往后n行末尾的所有内容，n=1,2,3...，如: 4y$ |

### paste

| 指令 | 说明 |
| :--: | :--- |
| `p` | 粘贴到当前位置后面或下一行 |
| `P` | 粘贴到当前位置前面或上一行 |
| `np` | 向后复制n次 |
| `nP` | 向前复制n次 |

### find/replace

| 指令 | 说明 |
| :--: | :--- |
| `/<PATTERN>` | 向下查找首个匹配项 |
| `?<PATTERN>` | 向上查找首个匹配项 |
| `n` | 向下查找匹配项 |
| `N` | 向上查找匹配项 |
| `*` | 向上查找与光标所在单词相同的单词 |
| `R` | 进入替换模式 |

### jump

| 指令 | 说明 |
| :--: | :--- |
| `h` | 左移一个字符 |
| `j` | 下移一行 |
| `k` | 上移一行 |
| `l` | 右移一个字符 |
| `gj` | 下移一个逻辑行 |
| `gk` | 上移一个逻辑行 |
| `gg` | 跳至首行 |
| `G` | 跳至尾行 |
| `w` | 跳至下一个单词的首字符 |
| `b` | 跳至上一个单词的首字符 |
| `e` | 跳至下一个单词的尾字符 |
| `ge` | 跳至上一个单词的尾字符 |
| `0` | 跳至当前行首个字符 |
| `^` | 跳至当前行首个非空字符 |
| `$` | 跳至当前行末尾 |
| `nG` | 跳至第n行 |
| `:n` | 跳至第n行 |

**说明：**在`vim`中，存在**逻辑行**和**物理行**两个概念，**物理行**指的是`:set number`后显示行号对应的行，**逻辑行**是单行显示不了后自动回绕自下一行产生的。

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