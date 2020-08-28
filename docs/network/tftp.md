# tftpd64

## Tftp server

若需要使用`tftp server`的功能时，首先需要对计算机中连接路由器的网卡设置静态`IP:192.168.1.10`，默认网关及`DNS`同样设为`192.168.1.1`（与路由器`LAN`端`IP`一致）；之后打开软件`tftpd64`，在`tftp server`界面设置相关参数：服务器的文件目录和接口。

![tftp server](../assets/tftp/tftpServer.png)

## Tftp client

若需要使用`tftp client`功能，向路由器烧写镜像文件的话，需要将`IP`设为`192.168.1.1`，`port`设为`69`（非必须）；然后需要选择好待烧写的镜像文件，并在路由器处于`upgrade mode`的状态下点击`put`按钮，完成镜像文件的烧写。

![tftp client](../assets/tftp/tftpClient.png)

路由器进入`upgrade mode`的两种情况：

1. 打开`console`，在路由器关机状态按住`reset`按键不放，单击开机键，等待`console`闪烁提示`upgrade mode`时放手；
2. 当刷机失败后重启时自动进入`upgrade mode`.
