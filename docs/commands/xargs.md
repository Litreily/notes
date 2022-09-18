# xargs

> xargs - build and execute command lines from standard input

## usage

`xargs`通常配合其它指令和管道一起使用，它将前面指令的输出结果作为下一个指令的输入，使用方法如下

```bash
command | xargs -item command
```

## examples

### 批量查找

```bash
find -name "*.c" |xargs grep -n "kerword"
```

### 批量复制

如果标准输入的信息是作为后续指令的前半部分参数的话，就需要使用`-I`参数指定其位置

```bash
find -name 'man1' | xargs -I {} cp {} $HOME/bin/local/share/man/
```
