# FAQ

<!-- toc -->

## 如何取消谷歌浏览器的秘钥环密码？

``` bash
seahorse
```
右键修改`Login`的`Passwords`为空即可。

## 点击链接后从谷歌浏览器打开空白页该如何解决？

谷歌浏览器的快捷方式可能有两个，一个在默认目录`/usr/share/applications`，另一个在目录`~/.local/share/applications/`，删除后面一个即可。

``` bash
rm ~/.local/share/applications/google-chrome.desktop
```