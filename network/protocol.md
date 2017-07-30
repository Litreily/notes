## 常见网络协议首部

<!-- toc -->

### IP

<table width="100%" style="text-align:center">
    <tr>
        <th colspan=4 width="50%">0~15</th>
        <th colspan=4 width="50%">16~31</th></tr>
    <tr>
        <td colspan=1 width="12.5%">4位版本</td>
        <td colspan=1 width="12.5%">4位首部长度</td>
        <td colspan=2 width="25%">8位服务类型</td>
        <td colspan=4 width="50%">16位总长度（字节）</td></tr>
    <tr>
        <td colspan=4 width="50%">16位标识</td>
        <td colspan=1 width="15%">3位标志</td>
        <td colspan=3 width="35%">13位片偏移</td></tr>
    <tr>
        <td colspan=2 width="25%">8位生成时间（TTL）</td>
        <td colspan=2 width="25%">8位协议</td>
        <td colspan=4 width="50%">16位首部校验和</td></tr>
    <tr>
        <td colspan=8 width="100%">32位源IP地址</td></tr>
    <tr>
        <td colspan=8 width="100%">32位目的IP地址</td></tr>
    <tr>
        <td colspan=8 width="100%">32位选项（若有）</td></tr>
    <tr>
        <td colspan=8 width="100%">数据</td></tr>
</table>

### UDP

<table width="100%" style="text-align:center">
    <tr>
        <th>0~15</th>
        <th>16~31</th></tr>
    <tr>
        <td>16位源端口号</td>
        <td>16位目的端口号</td></tr>
    <tr>
        <td>16位UDP长度</td>
        <td>16位UDP校验和</td></tr>
    <tr>
        <td colspan=2 width="100%">数据（若有）</td></tr>
</table>


### TCP

<table width="100%" style="text-align:center">
    <tr>
        <th colspan=16 width="50%">0~15</th>
        <th colspan=16 width="50%">16~31</th></tr>
    <tr>
        <td colspan=16 width="50%">16位源端口号</td>
        <td colspan=16 width="50%">16位目的端口号</td></tr>
    <tr>
        <td colspan=32 width="100%">32位序列号</td></tr>
    <tr>
        <td colspan=32 width="100%">32位确认号</td></tr>
    <tr>
        <td colspan=4 width="16%">4位首部长度</td>
        <td colspan=6 width="24%">6位保留</td>
        <td>URG</td>
        <td>ACK</td>
        <td>PSH</td>
        <td>PST</td>
        <td>SYN</td>
        <td>FIN</td>
        <td colspan=16 width="40%">16位窗口大小</td></tr>
    <tr>
        <td colspan=16 width="50%">16位TCP校验和</td>
        <td colspan=16 width="50%">16位紧急指针</td></tr>
    <tr>
        <td colspan=32 width="100%">选项（若有）</td></tr>
    <tr>
        <td colspan=32 width="100%">数据（若有）</td></tr>
</table>