# Link layer

<!-- toc -->

## 链路层的主要功能

* 为`IP`模块发送和接收`IP`数据报；
* 为`ARP`模块发送`ARP`请求和接收`ARP`应答；
* 为`RARP`发送`RARP`请求和接收`RARP`应答

## 相关术语

|   术语    | 含义                                                                                                                               |
| :-------: | :--------------------------------------------------------------------------------------------------------------------------------- |
|  以太网   | 数字设备公司(Digital Equipment Corp.)、英特尔公司（Intel Corp.）和Xerox公司在1982年联合公布的一个标准，采用`CSMA/CD`的媒体接入方法 |
| `CSMA/CD` | 带冲突检测的载波侦听多路访问技术<br>(Carrier Sense Multiple Access with Collision Detection)                                       |
|  `IEEE`   | 电气电子工程师协会<br>(Institute of Electrical and Electronics Engineers)                                                          |
|   `LLC`   | 逻辑链路控制<br>(Logical Link Control)                                                                                             |
|  `SLIP`   | 串行线路网际协议<br>(Serial Line IP)                                                                                               |
|   `PPP`   | 点对点协议<br>(Point to Point Protocol)                                                                                            |
|   `MAC`   | 媒体访问控制，硬件物理地址<br>(Media Address Control)                                                                              |
|   `MTU`   | 最大传输单元<br>(Maximum Transmission Unit)                                                                                        |

## IP数据报封装

* 以太网的`IP`数据报封装是在`RFC 894`（Hornig 1984）中定义的
* `IEEE 802`网络的`IP`数据报封装是在`RFC 1042`（Postel and Reynolds 1988）中定义的

封装格式详见[Protocol](./protocol.md#以太网)

## 最大传输单元

|             网络              | MTU字节 |
| :---------------------------: | :-----: |
|            超通道             |  65535  |
|     `16Mb/s`令牌环（IBM）     |  17914  |
| `4Mb/s`令牌环（`IEEE 802.5`） |  4464   |
|            `FDDI`             |  4352   |
|            以太网             |  1500   |
|      `IEEE 802.3/802.2`       |  1492   |
|            `x.25`             |   576   |
|       点对点（低时延）        |   296   |
