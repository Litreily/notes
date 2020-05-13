# ip

> show / manipulate routing, devices, policy routing and tunnels

## usage

``` zsh
➜  ip --help
Usage: ip [ OPTIONS ] OBJECT { COMMAND | help }
       ip [ -force ] -batch filename
where  OBJECT := { link | address | addrlabel | route | rule | neighbor | ntable |
                   tunnel | tuntap | maddress | mroute | mrule | monitor | xfrm |
                   netns | l2tp | fou | tcp_metrics | token | netconf }
       OPTIONS := { -V[ersion] | -s[tatistics] | -d[etails] | -r[esolve] |
                    -h[uman-readable] | -iec |
                    -f[amily] { inet | inet6 | ipx | dnet | mpls | bridge | link } |
                    -4 | -6 | -I | -D | -B | -0 |
                    -l[oops] { maximum-addr-flush-attempts } | -br[ief] |
                    -o[neline] | -t[imestamp] | -ts[hort] | -b[atch] [filename] |
                    -rc[vbuf] [size] | -n[etns] name | -a[ll] | -c[olor]}
```

## examples

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
