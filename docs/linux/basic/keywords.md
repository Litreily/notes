# Keywords

| auto | break | case | char|
|:---:|:---:|:---:|:---:|
| const | continue | default | do|
| double | else | enum | extern|
| float | for | goto | if|
| int | long | register | return|
| short | signed | sizeof | static|
| struct | switch | typedef | union|
| unsigned | void | volatile | while|

refer: <https://www.programiz.com/c-programming/list-all-keywords-c-language>


## typedef

``` c
typedef unsigned char BYTE;
BYTE b1, b2;

typedef struct {
    const unsigned char *json;
    size_t position;
} error;
error e1, e2;

typedef int * IntPtr;
IntPtr p1, p2, p3; // the type of p1, p2 and p3 are all the int *
```

## enum

``` c
enum color {
    RED,
    YELLOW,
    GREEN,
    BLUE,
    PINK
};

enum color newColor = BLUE;
```

``` c
typedef enum {
    RED,
    YELLOW,
    GREEN,
    BLUE,
    PINK
} color;

color newColor = BLUE;
```

``` c
enum color {
    RED,
    YELLOW,
    GREEN,
    BLUE,
    PINK
};

typedef enum color color;
color newColor = BLUE;
enum color oldColor = GREEN;
```

Other examples

``` c
enum boolean {false, true};
enum boolean check;
```

## union

`union` 占用内存大小取决于size最大的元素

``` c
union [union tag] {
    member definition;
    member definition;
    ...
    member definition;
} [one or more union variables];  
```

example:

``` c
union Data {
    int i;
    float f;
    char str[20];
} data;
// access data with data.i, data.f, data.str
// sizeof(data) == 20
```

## volatile

`volatile`防止因编译器优化导致变量读取错误的情况的发生。不加该关键词情况下，编译器可能会对某变量进行存储优化，将第一次存储的数据存入缓存，而后从缓存读取数据，但实际上该变量可能在以下情况发生了更改：

1. 信号处理程序
2. 硬件中断处理程序
3. 硬件交互(与内存映射IO相关)
4. 多线程中的其它线程修改了变量

添加关键词`volatile`后，编译器便知道这个变量是不稳定的，就会保证每次都从变量的原始地址读取数据。

``` c
volatile int i = 0;
volatile float * j = 1.0;
```

refer: [C/C++ volatile](https://blog.csdn.net/k346k346/article/details/46941497)

## register

> It's a hint to the compiler that the variable will be heavily used and that you recommend it be kept in a processor register if possible.
>
> Most modern compilers do that automatically, and are better at picking them than us humans.

refer: [“register” keyword in C?](https://stackoverflow.com/questions/578202/register-keyword-in-c)

简单点说，`register`告诉编译器，该变量会经常被用到，建议将其保存至CPU的寄存器中，以便快速读取。当然只是建议，编译器会依据情况看是否放入寄存器，而且现代编译器大多会自动选择将某变量存入内存还是寄存器。所以貌似用到的情况并不多见。

``` c
register int i = 0;

int j = 10;
register int * k = &j;
```

关于`register`：

1. 如果对`register`变量使用取地址符`&`，会引发编译错误，因为访问寄存器地址是无效的
2. `register`关键词可用于指针，此时使用`&`则不会报错
3. `register`是存储类，C语言不允许多个存储类关键词施加到一个变量，编译如下所示代码是会报错的
4. `register`只能作用于局部`block`，不能作用于全局变量
5. 理论上没有限制`register`变量个数，但编译器会选择性的存放至寄存器或内存中

``` c
int i = 10;
register static int * a = &i;
```

refer: [Understanding “register” keyword in C](https://www.geeksforgeeks.org/understanding-register-keyword/)

