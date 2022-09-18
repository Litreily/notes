# FAQ

<!-- toc -->

## U盘装机过程提示 “找不到任何设备驱动程序”

解决方法：

1. 回退至“现在安装”界面，选择“修复计算机”
2. 打开命令行工具
3. 输入`setup.exe`

其它尝试：

* 重新插拔 U 盘
* 切换`USB`口
* 切换 U 盘或系统镜像

## 使用固态硬盘，重新装机后无法正常关机和重启

解决方法：

1. 官方下载刷`BIOS`工具和文件（部分工具自带刷机包）
2. 重刷`BIOS`

## 多个网卡如何设置优先级

解决方法：

1. 针对win7, 可以在网络设置的高级设置中调整优先级
2. 针对win10, 可以修改各个网卡的IPv4属性中高级选项的跃点数，取消自动跃点，设置点数越高，优先级越低

## 无法打开 ACER 无线网卡

笔记本电脑不知何时起无法使用wifi了，尝试过很多方法都无法打开，我一度以为是硬件出问题了，后来很长一段时间都没有使用过无线。直到今天我想再更新一下驱动，安装驱动精灵扫描驱动，一切显示正常，但是就是打不开，快捷键`Fn F3`不管用。

但是驱动精灵显示有更新的驱动，不过网络原因没法更新成功，为此，我都是官网下载，在设备管理器获取到网卡型号

* qualcomm Atheros AR5B97

谷歌到对应网卡驱动下载网址

* <https://www.ath-drivers.eu/download-driver-nr-343-for-atheros-AR5B97-and-Windows10.html>

找到最新版驱动 [10.0.3.456](https://www.ath-drivers.eu/qualcomm-atheros-download-drivers-nr-343-with-code-3717.html) 下载更新后，一切恢复正常，快捷键又恢复了，完美。

## 家庭版无法使用远程桌面

安装 rdpwrap 解决。

```bash
# 管理员方式打开powershell
net stop termservice
# 修改或替换文件后
net start termservice
```

reference: 

- [Win10多用户远程桌面软件RDP Wrapper Library下载安装教程](https://blog.csdn.net/KotaTsuchiya/article/details/102908397)
- [Version 10.0.19041.964 Not Supported](https://github.com/stascorp/rdpwrap/issues/1384)

安装后 ubuntu 可使用系统自带 `remmina` 连接。