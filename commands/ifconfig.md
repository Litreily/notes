# ifconfig

``` bash
# show network interface info
ifconfig [interface]

# 添加ip addr
sudo ifconfig enp4s0f0 10.0.0.138 netmaask 255.255.255.0
sudo ifconfig enp4s0f0 inet6 add 2001:470:19:1316::1/64

# down/up interface
sudo ifconfig enp4s0f0 down
sudo ifconfig enp4s0f0 up
```

