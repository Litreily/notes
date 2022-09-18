# Protocol

<!-- toc -->

## 分层协议

| `TCP/IP` 模型 | 常用协议                                                               |
| :-----------: | :--------------------------------------------------------------------- |
|    应用层     | `DHCP`，`DNS`，`FTP`，`HTTP`，`IMAP`，`POP3`，`SMTP`，`SNMP`，`Telnet` |
|    传输层     | `TCP`，`UDP`                                                           |
|    网络层     | `IPv4`，`IPv6`，`ICMP`，`IGMP`                                         |
|    链路层     | 以太网，`IEEE 802`，`ARP`，`RARP`，`PPP`，`SLIP`                       |
|    硬件层     | ---                                                                    |

## 链路层

### 以太网

<table widtd="100%" style="text-align:center">
    <tr>
        <th>目的地址<br>6</th>
        <th>源地址<br>6</th>
        <th>类型<br>2</th>
        <th colspan=4>数据<br>46~1500</th>
        <th>CRC<br>4</th></tr>
    <tr>
        <td colspan=2></td>
        <td>0x0800<br>2</td>
        <td colspan=4>IP数据报<br>46~1500</td>
        <td></td></tr>
    <tr>
        <td colspan=2></td>
        <td>0x0806<br>2</td>
        <td colspan=3>ARP请求/应答<br>28</td>
        <td colspan=1>PAD<br>18</td>
        <td></td></tr>
    <tr>
        <td colspan=2></td>
        <td>0x0835<br>2</td>
        <td colspan=3>RARP请求/应答<br>28</td>
        <td colspan=1>PAD<br>18</td>
        <td></td></tr>
</table>

### IEEE 802.3

<table widtd="100%" style="text-align:center">
    <tr>
        <th colspan="3">802.3 MAC</th>
        <th colspan="3">802.2 LLC</th>
        <th colspan="2">802.2 SNAP</th>
        <th colspan="4"></th></tr>
    <tr>
        <td>目的地址<br>6</td>
        <td>源地址<br>6</td>
        <td>长度<br>1</td>
        <td>DASP<br>1</td>
        <td>SSAP<br>1</td>
        <td>cntl<br>1</td>
        <td>org code<br>3</td>
        <td>类型<br>2</td>
        <td colspan=3>数据<br>38~1492</td>
        <td>CRC<br>4</td></tr>
    <tr>
        <td colspan=7></td>
        <td>0x0800<br>2</td>
        <td colspan=3>IP数据报<br>38~1492</td>
        <td></td></tr>
    <tr>
        <td colspan=7></td>
        <td>0x0806<br>2</td>
        <td colspan=2>ARP请求/应答<br>28</td>
        <td>PAD<br>10</td>
        <td></td></tr>
    <tr>
        <td colspan=7></td>
        <td>0x0835<br>2</td>
        <td colspan=2>RARP请求/应答<br>28</td>
        <td>PAD<br>10</td>
        <td></td></tr>
</table>

### ARP

| HW type | Protocol type | HW size | Protocol size | Opcode | Sender MAC | Sender IP | Target MAC | Target IP |
| :-----: | :-----------: | :-----: | :-----------: | :----: | :--------: | :-------: | :--------: | :-------: |
|    2    |       2       |    1    |       1       |   2    |     6      |     4     |     6      |     4     |

**说明：**

* `HW`代表硬件(Hardware)
* `Opcode`: 1 → `ARP`请求，2 → `ARP`应答，3 → `RARP`请求，4 → `RARP`应答

## 网络层

### IPv4

* [RFC 791](https://tools.ietf.org/html/rfc791#section-3.1)

```yml
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version|  IHL  |Type of Service|          Total Length         |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Identification        |Flags|      Fragment Offset    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Time to Live |    Protocol   |         Header Checksum       |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                       Source Address                          |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Destination Address                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

**说明：**

* 8位`protocol`: 1 → `ICMP` ，2 → `IGMP` ，6 → `TCP` ，17 → `UDP`
* 首部校验和：先将校验和置零，然后以`16bit`为一个单元，对首部所有单元进行反码求和，结果存入校验和；接收端进行校验时同样对首部进行反码求和，求和结果应当为全1。

### IPv6

* [RFC 2460](https://tools.ietf.org/html/rfc2460)

```yml
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|Version| Traffic Class |           Flow Label                  |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|         Payload Length        |  Next Header  |   Hop Limit   |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                         Source Address                        +
|                                                               |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                                                               |
+                      Destination Address                      +
|                                                               |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

## 传输层

### UDP

* [RFC 768](https://tools.ietf.org/html/rfc768)

```yml
 0      7 8     15 16    23 24    31
+--------+--------+--------+--------+
|     Source      |   Destination   |
|      Port       |      Port       |
+--------+--------+--------+--------+
|                 |                 |
|     Length      |    Checksum     |
+--------+--------+--------+--------+
|
|          data octets ...
+---------------- ...
```

### TCP

* [RFC 793](https://tools.ietf.org/html/rfc793#section-3.1)

```yml
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|          Source Port          |       Destination Port        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                        Sequence Number                        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Acknowledgment Number                      |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|  Data |           |U|A|P|R|S|F|                               |
| Offset| Reserved  |R|C|S|S|Y|I|            Window             |
|       |           |G|K|H|T|N|N|                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|           Checksum            |         Urgent Pointer        |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                    Options                    |    Padding    |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             data                              |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

## 应用层

### 端口号

|   Process    |  PORT  |
| :----------: | :----: |
|  FTP Server  |   21   |
|   SSH, SCP   |   22   |
|    Telnet    |   23   |
| SMTP Server  |   25   |
|  DNS Server  |   53   |
| DHCP Server  | 67, 68 |
|     TFTP     |   69   |
| HTTP Server  |   80   |
| POP3 (Email) |  110   |
| HTPPS Server |  443   |
