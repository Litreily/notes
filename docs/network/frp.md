# frp

## 前提

- 带有公网IP的云服务器，我使用的是阿里云服务器
- 内网服务器
- 远程访问内网的客户端

## 下载 frp

- github: <https://github.com/fatedier/frp>

在github中找到最新 [frp Release](https://github.com/fatedier/frp/releases)，在公网服务器和内网服务器上都要下载。

```bash
wget https://github.com/fatedier/frp/releases/download/v0.44.0/frp_0.44.0_linux_amd64.tar.gz
tar -xvf frp_0.44.0_linux_amd64.tar.gz
cd frp_0.44.0_linux_amd64
```

## 配置 frp server

在公网服务器上解压frp服务程序，执行以下指令启动frp服务。

```bash
./frps -c ./frps.ini
```

需要修改端口的下，修改 `frps.ini` 文件即可，默认内容如下：

```ini
[common]
bind_port = 7000
```

## 配置 frp client

```bash
[common]
server_addr = 100.21.100.22
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000
```

启动客户端

```bash
./frpc -c ./frpc.ini
```

## 配置公网服务器的安全组

在公网服务器中需要添加安全组规则，添加端口(`7000`, `6000`)的安全规则，否则防火墙规则默认会挡掉连接。

## 远程访问内网

```bash
ssh -p 6000 username@serverip
```