# TeraTerm

## 宏语法

### connect

`connect`指令用于连接远程主机，后面的参数以`\`开始

``` bash
/C=3                连接串口COM3
/BAUD=115200        设置波特率
/F=TERATERM.INI     选择配置文件
/L=C:\test.log      选择日志存储文件，如果已经打开了`teraterm`的日志记录功能，可以不设置该项
```

更加详细的说明可以参考官方文档: <http://www.teraterm.net/manual/en/commandline/teraterm.html>

下面是连接串口COM3的一个示例：

``` bash
connect '/C=3 /BAUD=115200 /F=TERATERM.INI /L=C:\test.log'  
```

### sendln

`sendln`是发送消息的指令，如果连接的是串口，通过这个指令可以发送包含换行符的消息，与在`TeraTerm`中手动输入指令的效果一致。

``` bash
sendln "cd /bin"
sendln "ls"
```

### wait

`wait`用于等待指定字符串的出现，超时时间由`timeout`指定，当`timeout`小于0时代表无限等待；

``` bash
timeout=-1  ; not necessery
wait "Hit any key to stop autoboot"
```

`waitln`与`wait`略有不同，它会等待匹配到字符串后出现换行符方才执行后续指令，并将匹配行存入`TeraTerm`的系统变量`inputstr`中。

### pause

`pause`是暂停指令，相当于`bash`中的`sleep`，后面接暂停的时间，可以用于定时等待

``` bash
; sleep 5 minutes
pause 300
```

### end

`end`代表从当前脚本退出，可放于任意位置

### log

关于日志，除了使用`connect`中的`/L`指定日志文件外，还可以在脚本中对日志进行打开，关闭，暂停，重启等操作

``` bash
logopen "C:\Test.log" 0 0
logwrite "Test 1"#13#10
logwrite "Test 2"#13#10
logwrite "Test 3"#13#10
logpause
wait "Resetting to Default..."
logstart
logclose
```

值得注意的是，`logwrite`并不自动添加换行符，所以需手动添加，在`TeraTerm`中的换行符用`#13#10`表示。

## 结构指令

### do loop

``` c
do [ { while | until } <expression> (option)]
  ...
  ...
loop [ { while | until } <expression> (option)]
```

`do loop`类似于`C`语言中的`do while`

``` c
; Repeat ten times.
i = 10
do while i>0
    i = i - 1
loop
; Send clipboard content.
offset = 0
do
    clipb2var buff offset
    if buff > 0 send buff
    offset = offset + 1
loop while result = 2
```

### while

``` c
while <expression>
  ...
  ...
endwhile
```

``` c
; Repeat ten times.
i = 10
while i>0
  i = i - 1
endwhile
```

### if

`if, else, elseif, endif`有两种使用方式：

``` c
if <expression> <statement>
```

如`if A>1 goto label`，另一种方式如下：

``` c
if <expression 1> then
  ...
  (Statements for the case:  <expression 1> is true (non-zero).)
  ...
[elseif <expression 2> then]
  ...
  (Statements for the case:  <expression 1> is false (zero) and <expression 2> is true.)
  ...
[elseif <expression N> then]
  ...
  (Statements for the case:  <expression 1>, <expression 2>,... and <expression N-1> are all false, and <expression N> is true.)
  ...
[else]
  ...
  (Statements for the case:  all the conditions above are false (zero).)
  ...
endif
```

``` c
if a=1 then
  b = 1
  c = 2
  d = 3
endif

if i<0 then
  i=0
else
  i=i+1
endif

if i=1 then
  c = '1'
elseif i=2 then
  c = '2'
elseif i=3 then
  c = '3'
else
  c = '?'
endif
```

### for

``` c
for <intvar> <first> <last>
  ...
  ...
next
```

`for`循环的参数按1递增或递减

``` c
; Repeat ten times.
for i 1 10
  sendln 'abc'
next

; Repeat five times.
for i 5 1
  sendln 'abc'
next
```

## 函数定义

冒号`:`开头接函数名，`return`结尾，中间是函数体

``` bash
:FunctionName
    body
return
```

调用函数可以使用`call`指令:`call FunctionName`

## 注释

分号`;`开头的表示注释

``` bash
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
; Description : This is a comment
; Author : Guangtao.Wu
;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
```

## 宏脚本实例

### 定时重启路由器

``` bash
; loop reboot, pause 240s

connect /C=3 /BAUD=115200 /F=TERATERM.INI

while 1
    sendln "show console"
    sendln "reboot"
    pause 240
endwhile

end
```

如果已经打开某个或多个串口连接时，可以不用使用`connect`指令，这样便可以在多个窗口中同时使用相同的宏脚本，实现多个路由器自动定时重启。

### 反复重刷高低版本的路由器FW

``` bash
connect '/C=3 /BAUD=115200'

while 1
  call uBoot
  sendln "tftpboot 0x84000000 RBS20-V1.12.0.38.img"
  pause 20
  sendln "nand erase 0x3080000 0x2800000;"
  pause 15
  sendln "nand write 0x84000080 0x3080000 0x2800000;"
  pause 20
  sendln "reset"
  pause 300
  
  call uBoot
  sendln "tftpboot 0x84000000 RBS20-V2.1.0.34-RC2.img"
  pause 20
  sendln "nand erase 0x3080000 0x2800000;"
  pause 15
  sendln "nand write 0x84000080 0x3080000 0x2800000;"
  pause 20
  sendln "reset"

  offset=0
  do
    pause 300
    sendln "show console"
    sendln "reboot"
    offset = offset + 1
  loop while offset < 5
  
endwhile

exit

:uBoot
  sendln "show console"
  sendln "reboot"
  wait "Hit any key to stop autoboot"
  sendln "k"
  pause 6
return
```

## 运行宏

运行编写好的宏脚本主要有以下两种方法：

1. `TeraTerm`菜单栏中，选择“控制(O)”，然后选择“宏”，最后选择宏脚本开始执行；
2. 使用`CMD`，进入`TeraTerm`安装目录，执行`ttpmacro.exe scriptName.ttl`

## 参考文档

* <http://www.teraterm.net/manual/en/>
* <http://www.teraterm.net/manual/en/macro/command/index.html>
