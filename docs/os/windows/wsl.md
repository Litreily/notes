# WSL

## win11 install wsl2

```bash
C:\Users\guangtao.wu>wsl --install
适用于 Linux 的 Windows 子系统已安装。

以下是可安装的有效分发的列表。
请使用“wsl --install -d <分发>”安装。

NAME               FRIENDLY NAME
Ubuntu             Ubuntu
Debian             Debian GNU/Linux
kali-linux         Kali Linux Rolling
SLES-12            SUSE Linux Enterprise Server v12
SLES-15            SUSE Linux Enterprise Server v15
Ubuntu-18.04       Ubuntu 18.04 LTS
Ubuntu-20.04       Ubuntu 20.04 LTS
OracleLinux_8_5    Oracle Linux 8.5
OracleLinux_7_9    Oracle Linux 7.9

C:\Users\guangtao.wu>wsl --install -d Ubuntu-18.04
正在安装: Ubuntu 18.04 LTS
已安装 Ubuntu 18.04 LTS。
正在启动 Ubuntu 18.04 LTS…

C:\Users\guangtao.wu>
```

## error-1

```log
WslRegisterDistribution failed with error: 0x800701bc
```

解决方案：[win10 WSL2问题解决WslRegisterDistribution failed with error: 0x800701bc](https://blog.csdn.net/qq_18625805/article/details/109732122)

## error-2

```log
Installing, this may take a few minutes...
WslRegisterDistribution failed with error: 0x80370102
Please enable the Virtual Machine Platform Windows feature and ensure virtualization is enabled in the BIOS.
For information please visit https://aka.ms/enablevirtualization
Press any key to continue...
```

解决方案：控制面板->程序与功能->启用或关闭Windows功能->开启 `Hyper-V` 功能

