# Makefile

## 基本语法

### make 指令参数

- `-n` : 只打印编译过程，不执行指令，方便调试查看编译过程
- `-w` : 在编译是打印 `Entering directory ...` 信息，方便查看当前执行路径
- `-j` : 指定多核编译，加快编译速度
- `-t` : touch，更新明白文件的时间，但不更改文件
- `-I` : 指定一个搜索路径
- `-d` : 打印debug信息，帮助分析调试

### 变量

- `:=` : 变量赋值为新的值，`Foo:=bar`
- `?=` : 如果没有定义过则赋值新值，`Foo?=bar`
- `+=` : 追加变量值
- `empty :=` : 空变量
- `space := $(empty) $(empty)` : 空格变量
- `$(foo:.o=.c)` : 变量替换，将 `*.o` 替换为 `*.c`
- `$(foo:%o=%c)` : 静态模式的变量替换，将 `%.o` 替换为 `%.c`
- `$($(x))` : 变量值作为新变量名
- `y = $(subst a,b,$(x))` : 将变量x中的a替换为b，赋值给y
- `override` : 重写make命令行传入的参数值
- `define` : 定义多行变量

自动化变量：

- `$@` : 目标文件集
- `$%` : 目标成员名
- `$<` : 依赖目标中的首个目标名称
- `$?` : 所有比目标新的依赖目标的集合
- `$^` : 所有依赖目标的集合，自动去除重复目标
- `$+` : 与 `$^` 类似，但不去除重复的依赖目标
- `$*` : 目标模式中`%`与之前的部分

### 条件判断

- `ifeq`, `ifneq` : 判断变量是否等于或不等于某值
- `ifdef`, `ifndef` : 判断是否定义或未定义某变量

### 使用函数

- `$(<function> <args>)` : 调用函数, 参数间逗号分隔

字符串相关：

- `subst` : 字符串替换
- `patsubst` : 模式字符串替换
- `strip` : 去除字符串首尾空字符
- `findstring` : 查看字符串子串
- `filter` : 过滤函数，模式匹配
- `filter-out` : 反过滤函数，去除匹配到的参数

单词相关：

- `sort` ： 按单词排序
- `word` : 取单词函数，指定字符串第n个单词
- `wordlist` : 取单词串函数，指定起始位置和结束位置
- `words` : 统计单词个数
- `firstword` : 获取首个单词

文件目录相关：

- `dir` ：取目录路径
- `notdir` : 取文件名
- `suffix` : 取文件名后缀
- `basename` : 取文件路径的前缀
- `addsuffix` : 添加后缀
- `addprefix`: 添加前缀
- `join` : 连接字符串

循环或函数调用相关：

- `foreach` : 循环
- `if` : 条件判断
- `call` : 调用其它函数
- `shell` : 执行 shell 指令

make 执行控制相关：

- `error` : 产生错误信息，停止编译
- `warnning` : 产生警告信息，继续编译

## DEPENDS

在openwrt中，package可能会依赖一个或多个其它package，通过使用DEPENDS去定义依赖。

举例说明，当前有 package 名为 `demo_pack`, 依赖了两个package，`pack_a`, `pack_b`, 那么需要在Makefile中添加`DEPENDS`。

```Makefile
define Package/demo_pack
    DEPENDS:=+pack_a +pack_b
endef
```

在编译FW之前，需要在 buildroot 目录生成 .config 文件，通常会调用`make oldconfig`指令完成。这个指令会遍历所有packages，并根据Makefile确定依赖关系，这关系到不同package的编译顺序。

默认情况下，`make`过程根据package名称从小到大排序(a-z), demo_pack 以d开头，先于 `pack_a`, `pack_b`, 但是添加依赖以后，编译时会更改编译顺序，先编译其依赖库`pack_a`, `pack_b`, 之后再编译 `demo_pack`.

添加依赖包含以下几种方式：

1. `DEPENDS:=+pack_a` 表示只要选中了 `demo_pack`, `pack_a` 就会强制被选中，该方式最常用
2. `DEPENDS:=pack_a` 表示只有选中 `pack_a` 之后，才可以选中 `demo_pack`
3. `DEPENDS:=+FUNC_HAVE_A:pack_b` 表示只有选中 `FUNC_HAVE_A` 之后，才可以选中 `pack_b`
4. `DEPENDS:=@pack_a` 表示除非先选中 `pack_a`, 否则别想在menuconfig中看到 `demo_pack`, 不推荐
5. `DEPENDS:=+@pack_a` 与 `+pack_a` 类似，不同在于，在安装 `demo_pack` 时不会检查依赖性，`pack_a` 没有被安装是无法识别的

这里要说明的是，第3种方式在某些特定情况下非常有用。比如存在多个项目(A,B)，基于相同的code base，但是又有差异(使用不同的.config)，假设项目A中的CONFIG `FUNC_HAVE_A` 为 `y` ， `pack_b` 需要在该CONFIG选中情况下才生效，但项目B不需要支持 `pack_b`, 同时 `FUNC_HAVE_A` is not set 。这种情况下，如果使用以下依赖方式，

```Makefile
define Package/demo_pack
    DEPENDS:=+pack_b
endef
```

项目A可以正常编译和工作，但是对项目B而言，根据以上第1个选项的说明， make oldconfig 同样也会给项目B默认选中 `pack_b` ，这是我们不想要的。此时，使用 `+FUNC_HAVE_A:pack_b` 就再合适不过了。

```Makefile
define Package/demo_pack
    DEPENDS:=+FUNC_HAVE_A:pack_b
endef
```

这样既保证需要支持 `pack_b` 的项目A在 `make oldconfig` 时可以正确添加依赖库，又可以防止不需要支持的项目B不会默认选中 `pack_b`.

- 参考：[OpenWRT的包依赖 package DEPEND](http://blog.chinaunix.net/uid-27057175-id-5011775.html)