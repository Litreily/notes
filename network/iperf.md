# iperf3

## Description

`iperf3` 是一款网络性能测试工具，支持windows, linux, mac平台。相比于`IxChariot`而言简单易用

## Command

``` bash
# server
iperf3 -s

# [client -> server] client upload test
iperf3 -c <server-ip> -t <time> -P <process-num>
# [server -> client] client download test
iperf3 -c <server-ip> -t <time> -P <process-num> -R
```

## Example

``` bash
iperf3 -s  # server
iperf3 -c 10.0.0.1 -t 300 -P 8  # client
```
