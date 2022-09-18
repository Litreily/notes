# Ubuntu 双网卡做软路由

有两个网卡 `eth0`, `eth1`, `eth0` 连接外网上网，`eth1` 连接本地另外一台PC，需要共享 `eth0` 的网络给 `eth1`

## 配置静态IP

`eth1` 配置 `10.0.0.10` 静态IP，DNS与 `eth0` 一致。然后配置本地另一台PC IP为 `10.0.0.20`, DNS 设为 `8.8.8.8` 或者与 `eth0` 一致。

## fw.sh

编写以下脚本，实现网络共享，也就是简单的软路由。

```zsh
#!/bin/zsh
# let eth1 share the network from eth0

iptables -F FORWARD
iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
iptables -A FORWARD -i eth0 -o eth1 -m state --state ESTABLISHED,RELATED -j ACCEPT

iptables -t nat -F POSTROUTING
iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE
echo 1 > /proc/sys/net/ipv4/ip_forward
```

## reference

- [Ubuntu Server（18.04）开启路由转发搭建软路由](https://blog.csdn.net/Splend520/article/details/86505569)
