# ShadowSocks

## Chrome 使用 SwitchyOmega

如果是新系统，安装 Chrome 浏览器后默认无法打开应用商店，也就无法安装`SwitchyOmega`代理插件，此时需要有两种方案

### 方案一 - 开发者模式

1. 使用其它搜索引擎搜索下载`SwitchyOmega.crx`
2. 开启`Chrome`插件管理中的开发者模式`Developer mode`
3. 解压`.crx`文件, 在浏览器插件管理中选择已解压的插件(Load unpacked),选择解压的`SwitchyOmega.crx`文件夹

针对最新`Chrome`，该方案有个缺点，每次打开浏览器都会提示卸载以开发者模式启用的插件．

为了解决这个问题，可以最初不安装`SwitchyOmega`，而是以开发者模式安装该插件的前期版本`Proxy SwitchySharp`，使用该插件成功科学上网后，同步谷歌账号及插件（含SwitchyOmega），最后将该插件删除

### 方案二 - 全局代理

打开系统（假定 ubuntu）设置，选择`Settings -> Network -> Network Proxy`, 选择手动代理

![manual proxy](../assets/shadowsocks/manualProxy.png)

设置`Socks`代理为`127.0.0.1:1080`，此时浏览器便可以访问 Google 了，然后登录谷歌账号同步插件即可，如果之前账户并未安装该插件，则先打开`Chrome`的应用商店安装即可.

> 个人推荐方案二，简单快捷！

## 生成.pac 文件

如果想要在`ubuntu`系统下使用`ShadowSocks`的全局代理，需要使用到`.pac`文件，下面介绍此类文件的生成过程和使用方法。

首先保证系统已经安装`pip`

```sh
sudo apt install python-pip
```

然后使用`pip`安装`genpac`工具

```sh
sudo -H pip install genpac
```

接着使用`genpac`生成`autoproxy.pac`文件

```sh
sudo genpac --pac-proxy "SOCKS5 127.0.0.1:1080" \
--gfwlist-proxy="SOCKS5 127.0.0.1:1080" \
--gfwlist-url=https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt \
--output="autoproxy.pac"
```

生成以后，打开系统设置：`Settings -> Network -> Network Proxy`，选择`Automatic`，输入`.pac`文件的路径

```yml
Configuration URL: file:///home/username/shadowsocks/autoproxy.pac
```

### 注意

1. `:`后有三个`/`,`file://`对应文件协议，后面紧接文件路径
2. `ShadowSocks`设置的代理端口默认为`1080`，如果不是，需要修改以上指令的端口
3. 自动全局代理生效后，设置中的账户选项可能无法科学上网，反而使用手动设置全局代理可以，具体原因不清楚
