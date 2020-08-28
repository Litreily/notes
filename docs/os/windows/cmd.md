# cmd

## cmd alias

添加某些常用指令的别名，命名为cmd-alias.bat

``` batch
@echo off

:: cd
DOSKEY gk=cd E:\Guangtao.Wu\Desktop\Notebook

DOSKEY ls=dir /b $*
DOSKEY l=dir /od/p/q/tw $*
DOSKEY gb=gitbook build
DOSKEY up=shell.lnk upWeb

:: Git Aliases
DOSKEY gi=git init $*
DOSKEY gs=git status
DOSKEY ga=git add $*
DOSKEY gaa=git add --all
DOSKEY gpl=git pull $*
DOSKEY gph=git push $*
DOSKEY gplf=git pull --force $*
DOSKEY gphf=git push --force $*
DOSKEY gb=git branch $*
DOSKEY gbd=git branch -D $*
DOSKEY gcm=git commit -m $*
DOSKEY gco=git checkout $*
DOSKEY gri=git rebase -i $*
DOSKEY grir=git rebase --root -i
DOSKEY gcnf=git config $*
DOSKEY gcnf-user=git config user.name $*
DOSKEY gcnf-email=git config user.email $*
```

1. 将文件放置到一个固定目录，如C:\cmd-alias.bat
2. 将下面的执行存入一个`.reg`文件，然后执行它，此后打开`cmd`即可使其生效

``` reg
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Command Processor]
"AutoRun"="C:\cmd-alias.bat"
```

## netsh

公司电脑有两个有线网卡，分别为`Company`, `Router`，一个用于PC联网，一个用于测试。有时候为了测试路由器功能，需要频繁切换测试网卡为静态IP或动态IP，
或者启用/禁用网卡，需要每次都手动修改网络配置的话，效率太低，所以便有了以下脚本：

### EnableCompany.bat

``` batch
Echo off  
Echo Enable Company interface ...
Netsh interface Set interface "Company" enabled
```

### DisableCompany.bat

``` batch
Echo off  
Echo disabled Company interface ...
Netsh interface Set interface "Company" disabled
```

### DynamicIP.bat

``` batch
Echo off  

Echo getting Dynamic IP MASK GATEWAY ...
Netsh interface IP Set Addr "Router" dhcp

Echo getting Dynamic DNS
Netsh interface IP Set dns "Router" dhcp

Echo show config
Netsh interface IP show config "Router"

Echo done
```

### StaticIP.bat

``` batch
Echo off  

Echo setting IP MASK GATEWAY ...
Netsh interface IP Set Addr "Router" Static 192.168.1.10 255.255.255.0 192.168.1.1 1  

Echo setting DNS ...
Netsh interface IP Set dns "Router" static 192.168.1.1 primary  

Echo show config
Netsh interface IP show config "Router"

Echo done
```
