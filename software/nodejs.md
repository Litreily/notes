## 源码安装

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
sudo make	# 耗时较长
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

