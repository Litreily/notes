# Shell

<!-- toc -->

## 指令

### sudo

``` bash
sudo su  # 进入root模式
sudo <cmd> # 以管理员身份执行指令
```

### cd

``` bash
cd  # 回到默认目录 ~ ,即/home/user-name
cd ..  # 回退到前级目录
cd -  # 回退到前一次目录
cd <folder-path>  # 到达指定目录
```

### ls

``` bash
ls  # 显示当前路径下的文件及文件夹
ls -a  # 显示所有文件（包含隐藏文件及文件夹）
ls -F  # 在目录后显示'\'，在可执行文件后显示‘*’，便于区分文件及文件夹
ls -l  # 以长列表形式显示文件的详细信息
ls -R  # 递归显示文件和文件夹，以及子目录的文件及文件夹
```

### pwd

``` bash
pwd  # 显示当前路径
```

### mkdir

``` bash
mkdir <folder-name>  # 新建文件夹
```

### rm

``` bash
rm <file-name>  # 删除文件
rm -rf <folder-name>  # 删除文件夹
```

### df

``` bash
df -h  # 查看磁盘存储信息
```

### du

``` bash
du -sh  # 查看当前目录占用空间
du -h  # 查看当前目录及子目录下所有文件大小
```

### lsb_release

``` bash
$ lsb_release -a  # 查看当前系统版本信息
NO LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 16.04.3 LTS
Release:        16.04
Codename:       xenial
```

### fc-cache

``` bash
sudo mkdir /usr/share/fonts/custom
sudo cp /path/to/fontfile  /usr/share/fonts/custom
sudo chmod 644 /usr/share/fonts/custom/*

cd /usr/share/fonts/custom
sudo mkfontscale
sudo mkfontdir
sudo fc-cache -fv
```

### mount

挂载Samba共享服务

``` bash
sudo mkdir -p /mnt/smb
sudo mount -t cifs -o username=dnishare,password=sharedni -l //172.17.144.2/public /mnt/smb
```

## 配置

### 配置 bash

``` bash
vim ~/.bashrc
source .bashrc  # 记得使用source指令，否则更新内容无法生效
```

### tc

设置网络默认回包的延迟时间

``` bash
tc qdisc add dev eth0 root netem delay 6000ms
```

### ip

添加默认网关

``` bash
ip route add default via Gateway.addr
```

### 配置 zsh

使用[oh my zsh](https://github.com/robbyrussell/oh-my-zsh)

via curl

``` zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

via wget

``` zsh
sh -c "$(wget -O- https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

upgrade

``` zsh
upgrade_oh_my_zsh
```

