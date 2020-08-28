# FAQ

<!-- toc -->

## 如何取消谷歌浏览器的秘钥环密码

``` bash
seahorse
```

右键修改`Login`的`Passwords`为空即可。

## 点击链接后从谷歌浏览器打开空白页该如何解决

谷歌浏览器的快捷方式可能有两个，一个在默认目录`/usr/share/applications`，另一个在目录`~/.local/share/applications/`，删除后面一个即可。

``` bash
rm ~/.local/share/applications/google-chrome.desktop
```

## 禁止笔记本合盖后休眠

有时候需要通过ssh连接笔记本上的`ubuntu`，而笔记本则合盖就好，此时默认情况会进入休眠状态，进而导致ssh断开。解决方案如下：

1. settings -> power 中的blank screen选项中选择`never`，确保笔记本不定时锁屏
2. 执行以下执行防止合盖后休眠

``` bash
$ sudo vi /etc/systemd/logind.conf
# 将HandleLidSwitch一栏改为
HandleLidSwitch=ignore
$ sudo service systemd-logind restart
```

## 误删除 libc.so.6 怎么恢复

曾经为了在旧的Ubuntu系统上安装NTP server，需要更新GLIBC库到2.17，然后把`/lib/i386-linux-gnu/libc.so.6`给删了，删除之后发现基本上所有指令都无法使用了，简直崩溃啊！！！

删除后基本只能使用`cd` `pwd`这两个指令了，其它指令如`ls`, `mv`, `ln`等99%以上指令都无法使用。这是因为`libc.so.6`是非常底层的基本库，绝大多数指令都会用到。

那误删了怎么办，万能的Google让我搜到了相关的恢复方法，分两种情况，总结如下：

### root 用户

`root`用户的解决方案很简单，设置`LD_PRELOAD`变量后将`libc.so.6`重新设置为原先指向的库文件。

```bash
LD_PRELOAD=/lib/i386-linux-gnu/libc-2.15.so ln -s /lib/i386-linux-gnu/libc-2.15.so /lib/i386-linux-gnu/libc.so.6
```

其实`libc.so.6`本身就是个软链接，它指向GLIBC的库文件，如果删除后不知道版本号，不要着急，使用`LD_PRELOAD`变量后也可以使用其它指令，比如`ls`，哪怕不用ls，使用`tab`也可以显示目录文件，从中找出符合格式`libc-x.xx.so`的文件基本就是了。

### 非 root 用户

root 用户还是比较容易处理的，但是对于非`root`用户，没错，我遇到这个情况的时候就不是root用户，我是ssh远程过去的一个`common`用户，没有权限根本无法使用`ln`创建软链接，使用`sudo`也是无效的，因为sudo本身也依赖于这个库。

所以对于非root用户，我的解决方案是制作Ubuntu的U盘启动盘，强制关机后进入BIOS配置页面，选择U盘启动，然后在试用系统中执行了`ln`指令。

```bash
sudo ln -s /lib/i386-linux-gnu/libc-2.15.so /lib/i386-linux-gnu/libc.so.6
```

总算，一切恢复正常，从此不再手贱，同时立马给测试电脑启用了root用户，完美~
