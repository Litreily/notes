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
