# ip

``` bash
# 添加默认网关
sudo ip route add default via Gateway.addr

# 添加ip addr
sudo ip addr add 10.0.0.138/24 dev enp4s0f0

# 添加ipv6 addr
sudo ip -6 addr add 2001:470:19:1316::1/64 dev enp4s0f0
sudo ip -6 addr add local fe80::226a:8aff:fe6c:0fda/64 dev enp4s0f0

# 删除ip
sudo ip addr delete 10.0.0.138/24 dev enp4s0f0
sudo ip addr delete 2001:470:19:1316::1/64 dev enp4s0f0
sudo ip addr delete fe80::6096:7a4b:aeee:36af/64 dev enp4s0f0
```

