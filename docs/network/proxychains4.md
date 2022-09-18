# proxychains4

[proxychains4](https://github.com/rofl0r/proxychains-ng)是新一代的`proxychains`，非常强大的代理工具，一直用它来设置`socks5`在`Linux`系统的`Terminal`代理

## Install

``` sh
git clone https://github.com/rofl0r/proxychains-ng.git proxychains-ng.git
cd proxychains-ng.git
./configure --prefix=/usr --sysconfdir=/etc
make
sudo make install
sudo make install-config
```

最后一步用来生成配置文件`/etc/proxychains.conf`

## Config

打开`/etc/proxychains.conf`，将默认的`socks4`一行修改为

``` yml
socks5 127.0.0.1 1080
```

## Set alias

在`.bashrc`或是`.zshrc`中添加一行：

``` sh
alias supro="sudo proxychains4"
```

然后执行`source ~/.bashrc`生效

## Examples

``` sh
supro wget github.com
supro git clone https://github.com/rofl0r/proxychains-ng.git
```
