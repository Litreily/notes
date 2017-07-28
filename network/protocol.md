## 常见网络协议首部

### TCP

<table width="100%">
    <tr>
        <th width="50%">0~15</th>
        <th width="50%">16~31</th>
    </tr>
    <tr>
        <td>4位版本</td>
        <td>4位首部长度</td>
        <td>8位服务类型</td>
        <td>16位总长度（字节）</td>
    </tr>
    <tr>
        <td>16位标识</td>
        <td>3位标志</td>
        <td>13位片偏移</td>
    </tr>
    <tr>
        <td>8位生成时间（TTL）</td>
        <td>8位协议</td>
        <td>16位首部校验和</td>
    </tr>
    <tr>
        <td>32位源IP地址</td>
    </tr>
    <tr>
        <td>32位目的IP地址</td>
    </tr>
    <tr>
        <td>32位选项（若有）</td>
    </tr>
    <tr>
        <td>数据</td>
    </tr>
</table>

### UDP

### IP