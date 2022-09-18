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

## 支持网络服务器

如果内网中搭建了web服务器，也可以通过frp进行逆向代理。不过需要添加以下配置。

- frps.ini

```ini
[common]
server_addr = 100.21.100.22
server_port = 7000
vhost_http_port = 8080
```

- frpc.ini

```ini
[common]
server_addr = 100.21.100.22
server_port = 7000

[ssh]
type = tcp
local_ip = 127.0.0.1
local_port = 22
remote_port = 6000

[web]
type = http
local_port = 80
custom_domains = 100.21.100.22
```

> `custom_domains` 也可以是域名，不过需要添加对于DNS记录。

这样一来，就可以在浏览器输入 `http://公网服务器IP:8080` 访问内网站点了。

## 配置公网服务器的安全组

在公网服务器中需要添加安全组规则，添加端口(`7000`, `6000`, `8080`)的安全规则，否则防火墙规则默认会挡掉连接。

## 远程访问内网

```bash
ssh -p 6000 username@serverip
```