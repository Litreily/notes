# Watchdog

针对`openwrt`中的watchdog

## 禁用硬件watchdog

``` sh
devmem 0x0B017008 w 0x0
```

## watchdog软件控制指令

``` sh
# To query watchdog status
ubus call system watchdog

# To stop watchdog
ubus call system watchdog '{"stop": true}'

# To start watchdog
ubus call system watchdog '{"stop": false}'

# To configure watchdog timeout as 20 seconds (default is 30 seconds)
ubus call system watchdog '{"timeout": 20}'
```
