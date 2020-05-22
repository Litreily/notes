# Wireshark

## 常用过滤规则

``` yml
ip.addr == 192.168.1.1
http && ip.addr == 10.0.0.1
tcp.port == 8080
tcp.flags
udp
ftp
ntp
dns
bootp
igmp
arp
ppp || pppoe
icmp || icmpv6
```

## 找不到接口问题处理

> 以管理员身份运行CMD

``` bash
sc query npf # check npf status
net start npf # start npf
sc query npf # check npf status
```

## reassemble IP packet

wireshark  自动重组IP的分片报文，如果想要查看单独的分片信息，可以在`Preferences`的`Protocols`分组中选中`IPv4`,取消勾选"Reassemble fragmented Ipv4 datagrams"

## 设置接口的捕获过滤器

针对指定接口，在抓包之前可以通过捕获过滤器捕获指定的数据包。设置路径为：

`菜单栏->Capture->Options...`

进入对话框，选择指定Interface，在下面输入滤波器，比如设置“port 137”仅仅捕获NBNS数据包

![wireshark filter](/assets/wireshark/wireshark_filter.png)
