# man

## usage

```bash
man <command-name>
```

## MANPATH

linux系统中，除了最常用的环境变量`PATH`外，还包括`MANPATH`和`INFOPATH`等。

系统默认查询的man文件路径在`/etc/manpath.config`文件中定义，而`MANPATH`用于指定man手册存储路径，可以添加用户自定义的man文档。

比如手动安装`ctags`, `cscope`到指定路径`$HOME/bin/local/`后，需要显示man文档，就可以统一将文档移到`$HOME/bin/local/share/man`目录，然后在`.bashrc`文件中添加`MANPATH`

```bash
export MANPATH=$HOME/bin/local/share/man:$MANPATH
```

最后执行`source .bashrc`就ok了
