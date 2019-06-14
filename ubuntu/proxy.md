# Proxy

相信很多公司都有设置网络代理，而且需要密码认证，那么如果自带笔记本或是使用虚拟机，就需要对很多依赖网络的工具设置代理。

本文主要针对Linux系统，windows系统的代理设置相对单一些，通常设置好系统代理和浏览器代理即可。

## shell

要让`shell`使用代理，可以通过`cntlm`先配置好代理，默认安装`cntlm`后的配置文件为`/etc/cntlm.conf`

``` sh
Username    name
Domain      corp
Password    ********

Proxy       proxy_ip:port

Listen      3128
```

配置完后，执行下面的指令让代理生效

``` sh
sudo service cntlm restart
```

然后编辑`~/.bashrc`或其它shell的配置文件，我使用的zsh,所以修改`~/.zshrc`，添加代理

``` sh
export http_proxy="http://127.0.0.1:3128"
export https_proxy="http://127.0.0.1:3128"
export ftp_proxy="http://127.0.0.1:3128"
```

最后执行`source ~/.zshrc`,到此可以通过`wget www.baidu.com`验证代理是否可行。

大部分shell指令默认都会根据上面这几个参数去访问代理服务器，但是有些特殊的工具需要单独设置代理，包括`apt`,`git`,`npm`等，下面逐一介绍。

## apt

`apt` 或者 `apt-get`等工具的代理可以通过以下方式完成，这里同样是基于`cntlm`工具完成，文件`25apt`这个文件名可以任意，路径对了即可。

``` sh
$ sudo cat << EOF > /etc/apt/apt.conf.d/25apt
Acquire::http::proxy "http://127.0.0.1:3128/";
Acquire::https::proxy "http://127.0.0.1:3128/";
Acquire::ftp::proxy "http://127.0.0.1:3128/";
EOF
$ sudo apt update
```

如果使用的是其它代理工具，如`SS`，则将所有网络地址改成`http://127.0.0.1:1080`即可，前提是`SS`客户端配置的本地端口为`1080`.

## git

### https

```
# for http and https
git config --global http.proxy 'http://127.0.0.1:3128'
git config --global https.proxy 'http://127.0.0.1:3128'
# for git
git config --global core.gitProxy 'http://127.0.0.1:3128' 
```

### ssh

对于git操作，为了方便我们通常使用`ssh`协议，而不用`https`，这样可以省去每次输入用户名密码去push或是pull.这个可以参考文章[github ssh proxy协议代理配置](https://www.cnblogs.com/meshinestar/p/3994822.html)

1.配置一个`proxy-wrapper`脚本

```
$ cat > $HOME/bin/proxy-wrapper
#!/bin/zsh
nc -x 127.0.0.1:3128 -X connect $*
$ chmod +x $HOME/bin/proxy-wrapper
```

其中`-X`用于指定所用协议

- `-X4` - `socks4`
- `-X5` - `socks5`, 默认为该项
- `connect` - https, 需SSL支持，默认经443端口

2.配置`~/.ssh/config`

``` sh
Host github github.com
    Hostname github.com
    User    git
    ProxyCommand    $HOME/bin/proxy-wrapper %h %p
```

3.通过`ssh git@github.com`测试连接

这里需要说明的是，如果要使用https，那就需要ssl的支持，默认对应443端口，公司网络通常是禁用的，我尝试过，会提示安全问题：

> nc: Proxy error: "HTTP/1.1 502 Proxy Error ( The specified Secure Sockets Layer (SSL) port is not allowed. Forefront TMG is not configured to allow SSL requests from this port. Most Web browsers use port 443 for SSL requests.   )"nc: Proxy error: "HTTP/1.1 502 Proxy Error ( The specified Secure Sockets Layer (SSL) port is not allowed. Forefront TMG is not configured to allow SSL requests from this port. Most Web browsers use port 443 for SSL requests.   )"

当然啦，如果有`SS`支持，就可以选择`socks5`协议，这样就没问题了。

## npm

``` sh
npm config set proxy http://127.0.0.1:3128
npm config set https-proxy http://127.0.0.1:3128
npm config set registry http://registry.npm.taobao.org
```

貌似cntlm不支持https，所以需要在设置`npm`代理时将镜像源地址改为`http`协议

## 浏览器

大部分浏览器可以使用系统代理，但是在`ubuntu`的系统代理设置选项中，我没找到设置用户名密码的选项，所以另辟蹊径。

以Chrome浏览器为例，安装Proxy插件`SwitchyOmega`, 添加情景模式proxy，然后添加代理

![Chrome proxy](/assets/proxys/chrome-proxy.png)

如果使用的是其它代理工具，比如`Shadowsocks`，由于`SS`客户端通常将代理端口映射到本地的1080端口，所以这种情况只需要在`SwitchyOmega`中选择`sock5`协议，ip设为`127.0.0.1`,端口设为`1080`即可。关于这部分的详细内容参考我的另一篇文章[VPS+SS翻越GFW](https://www.litreily.top/2017/09/07/ss-config/)
