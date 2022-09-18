# ICMP

<!-- toc -->

## ICMP报文

`ICMP`报文封装在`IP`数据报内部。

 <table width="100%" style="text-align:center">
    <tr>
        <th colspan="1" width="25%">IP首部（20字节）</th>
        <th colspan="1" width="75%">ICMP报文</th>
    </tr>
</table>

其中`ICMP`报文格式如下：

<table width="100%" style="text-align:center">
    <tr>
        <th colspan="1" width="25%">0~7</th>
        <th colspan="1" width="25%">8~15</th>
        <th colspan="2" width="50%">16~31</th>
    </tr>
    <tr>
        <td colspan="1" width="25%">类型</td>
        <td colspan="1" width="25%">代码</td>
        <td colspan="2" width="50%">校验和</td>
    </tr>
    <tr>
        <td colspan="4" width="100%">不同类型和代码有不同的内容</td>
    </tr>
</table>

## ICMP地址掩码请求与应答

`ICMP`地址掩码请求用于无盘系统在引导过程中获取自己的子网掩码。系统广播`ICMP`请求报文，应答方以单播方式返回应答报文。其请求及应答报文格式如下：

<table width="100%" style="text-align:center">
    <tr>
        <th colspan="1" width="25%">0~7</th>
        <th colspan="1" width="25%">8~15</th>
        <th colspan="2" width="50%">16~31</th>
    </tr>
    <tr>
        <td colspan="1" width="25%">类型（17,18）</td>
        <td colspan="1" width="25%">代码（0）</td>
        <td colspan="2" width="50%">校验和</td>
    </tr>
    <tr>
        <td colspan="2" width="50%">标识符</td>
        <td colspan="2" width="50%">序列号</td>
    </tr>
    <tr>
        <td colspan="4" width="100%">32位子网掩码</td>
    </tr>
</table>

## ICMP时间戳请求与应答

`ICMP`时间戳请求允许系统向另一个系统查询当前时间，返回自午夜开始计算的毫秒数。其请求和应答报文格式如下：

<table width="100%" style="text-align:center">
    <tr>
        <th colspan="1" width="25%">0~7</th>
        <th colspan="1" width="25%">8~15</th>
        <th colspan="2" width="50%">16~31</th>
    </tr>
    <tr>
        <td colspan="1" width="25%">类型（13,14）</td>
        <td colspan="1" width="25%">代码（0）</td>
        <td colspan="2" width="50%">校验和</td>
    </tr>
    <tr>
        <td colspan="2" width="50%">标识符</td>
        <td colspan="2" width="50%">序列号</td>
    </tr>
    <tr>
        <td colspan="4" width="100%">发起时间戳</td>
    </tr>
        <td colspan="4" width="100%">接收时间戳</td>
    <tr>
    </tr>
        <td colspan="4" width="100%">传送时间戳</td>
    </tr>
</table>