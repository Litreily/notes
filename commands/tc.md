# tc

设置网络默认回包的延迟时间

``` bash
tc qdisc add dev eth0 root netem delay 6000ms
```
