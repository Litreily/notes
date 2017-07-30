## Ubuntu下的软件安装

### 添加PPA源
PPA 软件源的一般形式：`ppa:user/ppa-name`，添加方式如下

``` bash
sudo add-apt-repository ppa:user/ppa-name
sudo apt-get update
```

### apt-get
``` bash
sudo apt-get install <app-name>  # install
sudo apt-get remove <app-name>  # remove
```

### 安装 .Deb 文件
``` bash
dpkg -i <package-name>.deb
```

或者先安装 GDebi Package Installer
```
sudo apt-get install gdebi
```
然后用该安装工具进行安装。

### 安装 .tar.gz/.tar.xz 文件
``` bash
tar -xvzf <package-name>.tar.gz  # 解压.tar.gz文件
tar -xvJf <package-name>.tar.xz  # 解压.tar.xz文件
cd <package-path>  # 可参考包内的安装说明
./configure  # 部分压缩包已经编译过，可略过这一步
make
make install
```

### 安装.run文件

* 首先添加文件的执行权限
* 然后直接以`./<package-name>`方式安装

``` bash
chmod +x qt-opensource-linux-x64-5.8.0.run 
./qt-opensource-linux-x64-5.8.0.run 
```

## 添加快捷方式

为手动安装的软件添加快捷方式

``` bash
cd /usr/share/applications/
sudo vim <app-name>.desktop  # e.g. eclipse.desktop
```

输入内容
``` json
[Desktop Entry]
Encoding=UTF-8
Name=<app-name>  /* e.g. eclipse */
Comment=<comment-message> /* e.g. Eclipse IDE */
Exec=<app-path>  /* e.g. /opt/eclipse/eclipse */
Icon=<app-icon>  /* e.g. /opt/eclipse/icon.xpm */
Terminal=false  
StartupNotify=true  
Type=Application  
Categories=Application;Developmen;IDE;
```


## 常用软件

### 下载工具 uget+aria2
``` bash
sudo add-apt-repository ppa:plushuang-tw/uget-stable
sudo apt-get update
sudo apt-get install uget
```

``` bash
sudo add-apt-repository ppa:t-tujikawa/ppa
sudo apt-get update
sudo apt-get install aria2
```

打开 `uget` 软件，在设置选项的插件栏中选择 `aria2`.


### 微信

``` bash
git clone https://github.com/geeeeeeeeek/electronic-wechat.git
cd electronic-wechat
```

安装依赖包，两种方法
``` bash
npm install && npm start
```
or
``` bash
npm install electronic-packager
```

安装微信，安装过程需要下载文件（约 40M ）
``` bash
npm run build:linux
```
然后为其添加快捷方式即可

``` bash
sudo vim /usr/share/applications/wechat.desktop
```

``` json
[Desktop Entry]
Encoding=UTF-8
Name=Wechat
Comment=wechat
Exec=/home/litreily/Programs/Wechat/electronic-wechat
Icon=/home/litreily/Programs/Wechat/icon.png
Terminal=false
StartupNotify=true
Type=Application
Categories=Application;
```
