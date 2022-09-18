# ARP

<!-- toc -->

## 功能

`ARP`(Address Resolution Protocol)工作于**数据链路层**，为`IP`地址到对应的硬件`MAC`地址之间提供动态映射。

``` txt
32位Internet地址
    |    ^
ARP |    | RARP
    v    |
48位以太网MAC地址
```

## 特性

* 每个主机上都有一个`ARP`高速缓存，存放了最近Internet地址到硬件地址之间的映射记录；
* 每一项缓存的生存时间一般为20分钟;
* 分组格式见[protocol](./protocol.md#arp)

## 常用指令

``` bash
arp -a  # 显示ARP高速缓存
arp -d <IP-address>  # 删除某项高速缓存
arp -s <IP-address> <MAC-address> [temp]  #添加一项高速缓存
```
