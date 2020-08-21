# Protocol

<!-- toc -->

## 分层协议

| `TCP/IP`模型 | 常用协议                                                               |
| :----------: | :--------------------------------------------------------------------- |
|    应用层    | `DHCP`，`DNS`，`FTP`，`HTTP`，`IMAP`，`POP3`，`SMTP`，`SNMP`，`Telnet` |
|    传输层    | `TCP`，`UDP`                                                           |
|    网络层    | `IPv4`，`IPv6`，`ICMP`，`IGMP`                                         |
|    链路层    | 以太网，`IEEE 802`，`ARP`，`RARP`，`PPP`，`SLIP`                       |
|    硬件层    | ---                                                                    |

## 链路层

### 以太网

<table widtd="100%" style="text-align:center">
    <tr>
        <td>目的地址<br>6</td>
        <td>源地址<br>6</td>
        <td>类型<br>2</td>
        <td colspan=4>数据<br>46~1500</td>
        <td>CRC<br>4</td></tr>
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

<table widtd="100%" style="text-align:center">
    <tr>
        <td colspan=4 widtd="50%">0~15</td>
        <td colspan=4 widtd="50%">16~31</td></tr>
    <tr>
        <td colspan=1 widtd="12.5%">4位版本</td>
        <td colspan=1 widtd="12.5%">4位首部长度</td>
        <td colspan=2 widtd="25%">8位服务类型</td>
        <td colspan=4 widtd="50%">16位总长度（字节）</td></tr>
    <tr>
        <td colspan=4 widtd="50%">16位标识</td>
        <td colspan=1 widtd="15%">3位标志</td>
        <td colspan=3 widtd="35%">13位片偏移</td></tr>
    <tr>
        <td colspan=2 widtd="25%">8位生成时间（TTL）</td>
        <td colspan=2 widtd="25%">8位协议</td>
        <td colspan=4 widtd="50%">16位首部校验和</td></tr>
    <tr>
        <td colspan=8 widtd="100%">32位源IP地址</td></tr>
    <tr>
        <td colspan=8 widtd="100%">32位目的IP地址</td></tr>
    <tr>
        <td colspan=8 widtd="100%">32位选项（若有）</td></tr>
    <tr>
        <td colspan=8 widtd="100%">数据</td></tr>
</table>

**说明：**

* 8位协议: 1 → `ICMP` ，2 → `IGMP` ，6 → `TCP` ，17 → `UDP`
* 首部校验和：先将校验和置零，然后以`16bit`为一个单元，对首部所有单元进行反码求和，结果存入校验和；接收端进行校验时同样对首部进行反码求和，求和结果应当为全1。

## 传输层

### UDP

<table widtd="100%" style="text-align:center">
    <tr>
        <td>0~15</td>
        <td>16~31</td></tr>
    <tr>
        <td>16位源端口号</td>
        <td>16位目的端口号</td></tr>
    <tr>
        <td>16位UDP长度</td>
        <td>16位UDP校验和</td></tr>
    <tr>
        <td colspan=2 widtd="100%">数据（若有）</td></tr>
</table>

### TCP

<table widtd="100%" style="text-align:center">
    <tr>
        <td colspan=16 widtd="50%">0~15</td>
        <td colspan=16 widtd="50%">16~31</td></tr>
    <tr>
        <td colspan=16 widtd="50%">16位源端口号</td>
        <td colspan=16 widtd="50%">16位目的端口号</td></tr>
    <tr>
        <td colspan=32 widtd="100%">32位序列号</td></tr>
    <tr>
        <td colspan=32 widtd="100%">32位确认号</td></tr>
    <tr>
        <td colspan=4 widtd="16%">4位首部长度</td>
        <td colspan=6 widtd="24%">6位保留</td>
        <td>URG</td>
        <td>ACK</td>
        <td>PSH</td>
        <td>PST</td>
        <td>SYN</td>
        <td>FIN</td>
        <td colspan=16 widtd="40%">16位窗口大小</td></tr>
    <tr>
        <td colspan=16 widtd="50%">16位TCP校验和</td>
        <td colspan=16 widtd="50%">16位紧急指针</td></tr>
    <tr>
        <td colspan=32 widtd="100%">选项（若有）</td></tr>
    <tr>
        <td colspan=32 widtd="100%">数据（若有）</td></tr>
</table>

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
