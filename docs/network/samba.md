# Samba Server

`Samba`服务器可以完成Linux操作系统和Windows操作系统之间的文件共享，非常方便。

## 安装和卸载

``` bash
# install
sudo apt install samba samba-common

# uninstall
sudo apt install autoremove samba
```

## 创建共享目录

``` bash
sudo mkdir /home/share
sudo chmod 777 /home/share
```

在`home`创建一个单独目录`share`用于存储共享数据，并赋予全部读写执行权限

## 添加samba用户

``` bash
$ sudo smbpasswd -a litreily
New SMB password:
Retype new SMB password:
```

设置用户名和密码，示例的用户名是`litreily`

其它相关指令如下：

``` bash
# 删除用户
sudo smbpasswd -x litreily

# 禁用用户
sudo smbpasswd -d litreily

# 启用用户
sudo smbpasswd -e litreily
```

## 配置smb.conf

``` bash
$ sudo vi /etc/samba/smb.conf
# 在文件最后添加
[share]
   comment = share data
   path = /home/share
   browseable = yes
   writeable = yes
   valid users = litreily
   create mask = 0755
   directory mask = 0755
   guest ok = no
```

配置共享路径，文件及目录的读写权限，配置有效用户（注意用户名要设置为当前用户或者root），禁止访客访问

## 免密共享

如果想要完全公开，任何人都可访问的话，可以参考以下配置

``` bash
[share]
   comment = share data
   path = /home/share
   browseable = yes
   writeable = yes
   public = yes
   create mask = 0777
   directory mask = 0777
```

## 启动或重启Samba服务

``` bash
sudo /etc/init.d/smbd {start|stop|status|restart}
```

## 在Windows中访问Samba

在资源管理器中或`Win R`中输入`\\samba.host.ip\share`，比如`\\172.17.144.66\share`，然后输入用户名密码即可访问。

refer: [ubuntu下Samba服务器的搭建](https://blog.csdn.net/u012478275/article/details/78876181)
