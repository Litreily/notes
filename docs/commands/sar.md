# sar

> `sar` System Activity Reporter, 一款系统性能分析工具，对系统当前状态进行取样

## usage

```bash
➜  sar -h
Usage: sar [ options ] [ <interval> [ <count> ] ]
Main options and reports:
        -B      Paging statistics
        -b      I/O and transfer rate statistics
        -d      Block devices statistics
        -F      Filesystems statistics
        -H      Hugepages utilization statistics
        -I { <int> | SUM | ALL | XALL }
                Interrupts statistics
        -m { <keyword> [,...] | ALL }
                Power management statistics
                Keywords are:
                CPU     CPU instantaneous clock frequency
                FAN     Fans speed
                FREQ    CPU average clock frequency
                IN      Voltage inputs
                TEMP    Devices temperature
                USB     USB devices plugged into the system
        -n { <keyword> [,...] | ALL }
                Network statistics
                Keywords are:
                DEV     Network interfaces
                EDEV    Network interfaces (errors)
                NFS     NFS client
                NFSD    NFS server
                SOCK    Sockets (v4)
                IP      IP traffic      (v4)
                EIP     IP traffic      (v4) (errors)
                ICMP    ICMP traffic    (v4)
                EICMP   ICMP traffic    (v4) (errors)
                TCP     TCP traffic     (v4)
                ETCP    TCP traffic     (v4) (errors)
                UDP     UDP traffic     (v4)
                SOCK6   Sockets (v6)
                IP6     IP traffic      (v6)
                EIP6    IP traffic      (v6) (errors)
                ICMP6   ICMP traffic    (v6)
                EICMP6  ICMP traffic    (v6) (errors)
                UDP6    UDP traffic     (v6)
        -q      Queue length and load average statistics
        -R      Memory statistics
        -r      Memory utilization statistics
        -S      Swap space utilization statistics
        -u [ ALL ]
                CPU utilization statistics
        -v      Kernel tables statistics
        -W      Swapping statistics
        -w      Task creation and system switching statistics
        -y      TTY devices statistics

Options are:
[ -A ] [ -B ] [ -b ] [ -C ] [ -D ] [ -d ] [ -F ] [ -H ] [ -h ] [ -p ] [ -q ]
[ -R ] [ -r ] [ -S ] [ -t ] [ -u [ ALL ] ] [ -V ] [ -v ] [ -W ] [ -w ] [ -y ]
[ -I { <int> [,...] | SUM | ALL | XALL } ] [ -P { <cpu> [,...] | ALL } ]
[ -m { <keyword> [,...] | ALL } ] [ -n { <keyword> [,...] | ALL } ]
[ -j { ID | LABEL | PATH | UUID | ... } ]
[ -f [ <filename> ] | -o [ <filename> ] | -[0-9]+ ]
[ -i <interval> ] [ -s [ <hh:mm:ss> ] ] [ -e [ <hh:mm:ss> ] ]
```

## examples

```bash
# 每秒输出一次，共100次
➜  sar 1 100
Linux 3.14.77   09/30/18        _armv7l_        (4 CPU)

12:22:36        CPU     %user     %nice   %system   %iowait    %steal     %idle
12:22:37        all      0.50      0.00      1.26      0.00      0.00     98.24
12:22:38        all      1.02      0.00      0.76      0.00      0.00     98.22
12:22:39        all      0.25      0.00      0.76      0.00      0.00     98.99
12:22:40        all      0.76      0.00      1.02      0.00      0.00     98.22

# 打印所有CPU的占用情况
➜  sar 1 100 -P ALL
Linux 3.14.77   09/30/18        _armv7l_        (4 CPU)

12:23:22        CPU     %user     %nice   %system   %iowait    %steal     %idle
12:23:23        all      0.51      0.00      1.01      0.00      0.00     98.48
12:23:23          0      2.00      0.00      0.00      0.00      0.00     98.00
12:23:23          1      0.00      0.00      3.06      0.00      0.00     96.94
12:23:23          2      0.00      0.00      0.00      0.00      0.00    100.00
12:23:23          3      0.00      0.00      1.02      0.00      0.00     98.98

12:23:23        CPU     %user     %nice   %system   %iowait    %steal     %idle
12:23:24        all      0.00      0.00      1.50      0.00      0.00     98.50
12:23:24          0      0.00      0.00      1.00      0.00      0.00     99.00
12:23:24          1      0.00      0.00      2.02      0.00      0.00     97.98
12:23:24          2      0.00      0.00      0.00      0.00      0.00    100.00
12:23:24          3      0.00      0.00      2.97      0.00      0.00     97.03
```

## reference

- [sar 找出系统瓶颈的利器](https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/sar.html)
