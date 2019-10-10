# Preprocess

## include

``` c
#include <stdio.h>  // search from env path first
#include "user.h"   // search from local path first
```

## define

``` c
// #define is a C-directive which is used to define the aliases for data types
#define TRUE 1
#define FALSE 0

// typedef interpretation is performed by the compiler
typedef unsigned char BYTE
```

## if else

``` c
#if expression
#endif

#if expression1
#elif expression2
#elif expression3
#else
#endif

#ifdef expression
#else
#endif

#ifndef expression
#endif
```

## pragma

开源代码`cJSON.c`中用到以下语法，该语法用于设定外部连接实体的可见性`visibility`

``` c
#ifdef __GNUC__
#pragma GCC visibility push(default)
#endif

#include <string.h>
#include <stdio.h>
#include <math.h>
#include <stdlib.h>
#include <float.h>
#include <limits.h>
#include <ctype.h>
#include <locale.h>

#ifdef __GNUC__
#pragma GCC visibility pop
#endif
```

在以上代码中，两个`#pragma`之间的包含项便是外部链接实体，`push(default)`中的default可以有以下几个选择:

- **default**

指示受影响的外部链接实体具有默认可见性属性，这些实体将导出至共享库，也可以被抢占

- **protected**

指示受影响的外部链接实体具有受保护的可见性属性，这些实体将导出至共享库，但不能被抢占

- **hidden**

指示受影响的外部链接实体具有隐藏的可见性属性，这些实体不会导出至共享库，但是可以间接的通过指针访问它们的地址

- **internal**

指示受影响的外部链接实体具有内部可见的可见性属性，这些实体不会导出至共享库，它们的地址对其它模块也不可见

