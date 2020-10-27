# Weak Symbol

在C语言的库函数中，有时候会看到`weak_alias`函数，那么这是用来干什么的呢？先看其定义：

- `include/libc-symbols.h`

```c
/* Define ALIASNAME as a weak alias for NAME.
   If weak aliases are not availbale, this defines a strong alias. */
#  define weak_alias(name, aliasname) _weak_alias (name, aliasname)
#  define _weak_alias(name, aliasname) \
  extern __typeof (name) aliasname __attribute__ ((weak, alias (#name)));
```

`weak` 是 **弱**，`alias` 是 **别名** , 加一起就是 **弱别名**, 与之对应的有 **强别名**，强别名就是函数名本身，而弱别名相当于某个函数的别名。

举例说明，在库函数system() 对应的文件 `libc/stdlib.c/system.c` 中，其最后几行为:

```c
#ifdef IS_IN_libc
weak_alias(__libc_system,system)
#endif
```

这里定义了`__libc_system`的一个别名`system`, 那这个别名的意义何在呢？通常我们在写C代码时，如果要调用`system`函数，会先包含头文件`stdlib.h`, 然后直接调用`system`, 这时候编译器在库函数找不到以`system`命名的函数，但是找到这个弱别名的声明，知道了`system`函数对应的原函数是`__libc_system`, 那么最终就会调用`__libc_system` 函数。

简言之，就是一种简单的符号映射，把用户调用的函数名映射到库函数中实际实现功能的函数名。

## reference

- [Weak symbol - wikipedia](https://en.wikipedia.org/wiki/Weak_symbol)
- [C语言 : weak_alias描述](https://blog.csdn.net/weixin_39455835/article/details/80958105)
- [c - weak_alias函数做什么，它在哪里定义](https://www.coder.work/article/168442)
