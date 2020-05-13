# ping

``` bash
ping 192.168.1.1  # ping ipv4
ping baidu.com  # ping domain name
ping -6 ipv6  # ping ipv6 addr

# ping with timestamp
ping 192.168.1.1 |awk '{print $0"\t" strftime("%H:%M:%S",systime())}'
```

