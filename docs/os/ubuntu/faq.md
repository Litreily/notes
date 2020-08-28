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
