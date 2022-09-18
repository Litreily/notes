# Node.js

<!-- toc -->

## 安装 Node.js

### 源码安装

下载源码（300M左右）

``` bash
sudo git clone https://github.com/nodejs/node.git
```

修改目录权限

``` bash
sudo chmod -R 755 node
```

创建并编译文件

``` bash
cd node
sudo ./configure
sudo make   # 耗时较长
sudo make install
```

### apt-get 安装

``` bash
sudo apt-get install nodejs
sudo apt-get install -y build-essential
sudo apt-get install npm
sudo npm install n -g   # 安装用于更新管理nodejs的工具，该项可选
sudo n stable   # 获取最新稳定版的nodejs
```

### 官网下载安装

* 先到官网下载稳定版的`nodejs`,一般是`tar.xz`格式;
* 然后解压至本地目录（如：~/Programs/)
* 执行以下指令，若成功显示版本好，说明已经编译好，可以直接使用

``` bash
cd node-v6.11.0-linux-x64
./node -v
```

* 接下来配置环境变量，使其变为全局可用

``` bash
ln -s /home/litreily/Programs/node-v6.11.0-linux-x64/bin/node /usr/local/bin/node
ln -s /home/litreily/Programs/node-v6.11.0-linux-x64/bin/npm /usr/local/bin/npm
```

## npm换源

### 临时使用

``` bash
npm --registry https://registry.npm.taobao.org install express
```

### 永久使用

``` bash
npm config set registry https://registry.npm.taobao.org
npm config get registry  # 验证源
```
