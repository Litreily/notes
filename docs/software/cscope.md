# cscope

`cscope`是一款强大的用于源码分析的开发工具，可以快速定位变量、函数的定义和调用关系。

## install

下载 [cscope](http://cscope.sourceforge.net/#downloads) 后安装

```bash
tar -xvf cscope.tar.gz
cd cscope
./configure --prefix=/home/user/bin/local/cscope
make
make install
```

其中`prefix`可选，如果可以使用sudo的话就不需要了，如果只是给单个用户使用就可能会用到。

## config

为了在使用vim的时候自动加载`cscope.out`，可以在.vimrc中添加

```bash
" Set cscope
if has("cscope")
    set csprg=$HOME/bin/cscope " set cscope path
    set csto=1 " search tags file first, then search database of cscope
    set cst " use :cstag instead of default :tag
    set nocsverb
    if filereadable("cscope.out")
        cs add cscope.out
    endif
    set csverb
endif
```

## shortcut

cscope有很强大的跳转功能，默认需要使用`:cs find s`这样的指令去跳转，具体包含以下功能

```
a: Find assignments to this symbol
c: Find functions calling this function
d: Find functions called by this function
e: Find this egrep pattern
f: Find this file
g: Find this definition
i: Find files #including this file
s: Find this C symbol
t: Find this text string
```

为了简化跳转，可以在`.vimrc`中添加快捷映射，把指令映射为快捷键操作

```bash
noremap <leader>cs :cs find s 
noremap <C-\>a :cs find a <C-R>=expand("<cword>")<CR><CR>
noremap <C-\>c :cs find c <C-R>=expand("<cword>")<CR><CR>
noremap <C-\>d :cs find d <C-R>=expand("<cword>")<CR><CR>
noremap <C-\>e :cs find e <C-R>=expand("<cword>")<CR><CR>
noremap <C-\>f :cs find f <C-R>=expand("<cfile>")<CR><CR>
noremap <C-\>g :cs find g <C-R>=expand("<cword>")<CR><CR>
noremap <C-\>i :cs find i <C-R>=expand("<cfile>")<CR><CR>
noremap <C-\>s :cs find s <C-R>=expand("<cword>")<CR><CR>
noremap <C-\>t :cs find t <C-R>=expand("<cword>")<CR><CR>
```

其中`<cword>`代表当前所选的变量或函数，`<cfile>`代表当前文件。

将`cs find`指令统统映射到`<C-\>`，比如，`cs find s`被映射到`Ctrl-\ s`,也就是说按住Ctrl键和\键，松开再按s就可以查找当前所在变量或函数对应的符号表了。

此外，vim自带的跳转功能`ctrl-]`, `ctrl-i`, `ctrl-o`也会有所变化。

## usage

使用前需要先生成索引数据库, `R`代表递归，`b`代表仅生成库不弹出操作选项，`q`会生成缓存`cscope.in.out` `cscope.po.out`，可以加速索引。

```bash
cscope
cscope -Rb
cscope -Rbq
```

vim 下使用`:cs help`可以看到更详细的信息

```bash
cscope commands:
add  : Add a new database             (Usage: add file|dir [pre-path] [flags])
find : Query for a pattern            (Usage: find a|c|d|e|f|g|i|s|t name)
       a: Find assignments to this symbol
       c: Find functions calling this function
       d: Find functions called by this function
       e: Find this egrep pattern
       f: Find this file
       g: Find this definition
       i: Find files #including this file
       s: Find this C symbol
       t: Find this text string
help : Show this message              (Usage: help)
kill : Kill a connection              (Usage: kill #)
reset: Reinit all connections         (Usage: reset)
show : Show connections               (Usage: show)
Press ENTER or type command to continue
```

!!! note
    如果不是在vim中打开cscope，可以通过`Ctrl-d`退出操作界面。