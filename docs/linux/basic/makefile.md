# Makefile

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