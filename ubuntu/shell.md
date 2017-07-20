# 指令

## sudo
``` bash
sudo su  # 进入root模式
sudo {cmd} # 以管理员身份执行指令
```

## cd
``` bash
cd  # 回到默认目录 ~ ,即/home/user-name
cd ..  # 回退到前级目录
cd {folder-path}  # 到达指定目录
```


## ls
``` bash
ls  # 显示当前路径下的文件及文件夹
ls -a  # 显示所有文件（包含隐藏文件及文件夹）
ls -F  # 在目录后显示'\'，在可执行文件后显示‘*’，便于区分文件及文件夹
ls -l  # 以长列表形式显示文件的详细信息
ls -R  # 递归显示文件和文件夹，以及子目录的文件及文件夹
```

## pwd
``` bash
pwd  # 显示当前路径
```

## mkdir
``` bash
mkdir {folder-name}  # 新建文件夹
```

## rm
``` bash
rm {file-name}  # 删除文件
rm -rf {folder-name}  # 删除文件夹
```
