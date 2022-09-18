# mount

挂载Samba共享服务

``` bash
sudo mkdir -p /mnt/smb
sudo mount -t cifs -o username=dnishare,password=sharedni -l //172.17.144.2/public /mnt/smb

# bash on windows
sudo mount -t drvfs '\\172.17.144.2\public' /mnt/smb
```
