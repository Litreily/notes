# 安装vps系统后要做的事

本文以`centos 6.9`为例

## 上传本地RSA公钥

``` bash
ssh-keygen -t rsa
ssh-copy-id -i ~/.ssh/id_rsa/pub root@104.225.146.204
```

## 安装常用工具

``` bash
sudo yum install vim
sudo yum install git
sudo yum install zsh
sudo yum install gcc make automake

```

## 修改ssh超时时间

``` bash
$ vim /etc/ssh/sshd_config
ClientAliveInterval 60
ClientAliveCountMax 3
```

这样保证`ssh server` 每隔一分钟向`client`发送一个包，`client`通常会返回一个包，从而实现不间断访问。

## 安装tmux

``` bash
# install deps
yum install kernel-devel ncurses-devel

# install libevent
curl -OL https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz
tar -zxvf libevent-2.1.8-stable.tar.gz
cd libevent-2.1.8-stable
./configure && make
sudo make install

# install tmux
curl -OL https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz
tar -xzvf tmux-2.5
cd tmux-2.5
LDFLAGS="-L/usr/local/lib -Wl,-rpath=/usr/local/lib" ./configure --prefix=/usr/local
make
sudo make install

tmux -V
```

## 安装nginx server

`nginx server`相比`apache`，占用内存更少，应用更广。

``` bash
sudo yum install epel-release
sudo yum install nginx

# 可能出现显示epel-release已安装但无法安装nginx的情况
# 此时，可以执行以下指令

sudo rpm -e epel-release
sudo yum install epel-release
sudo yum install nginx

# nginx开机自启动
sudo /etc/init.d/nginx start
```
