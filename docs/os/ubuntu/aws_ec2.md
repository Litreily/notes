# AWS EC2

## Connect

### Linux ssh 指令登录

``` bash
ssh -i aws-ec2.pem ubuntu@host.ip
```

### Android 登录

`Android`端使用`JuiceSSH`客户端也可以登录，记得将`aws-ec2.pem`秘钥文件导入认证信息即可。

### Windows PuTTy登录

使用`PuTTy`登录，需要先通过`PuTTygen`将`.pem`文件转换为`.ppk`文件，然后打开`putty`，在 "Category/Connection/SSH/Auth" 配置栏的 "Private key file for authentication: "中输入`.ppk`文件路径，详细流程参考以下官方文档。

refer: [使用 PuTTY 从 Windows 连接到 Linux 实例](https://docs.aws.amazon.com/zh_cn/AWSEC2/latest/UserGuide/putty.html)

## 更换秘钥

首先在`aws`官网的控制台生成一个新的秘钥对，并下载新的`.pem`秘钥文件， 然后通过旧的秘钥文件ssh远程登录服务器，将新的秘钥文件存入服务器，导入方式有两种：

1. 方法一，在服务器新建`.pem`文件，然后把新的`.pem`文件内容复制进去，接着保存；
2. 方法二，使用scp指令

``` bash
scp -i aws-old.pem aws-new.pem ubuntu@host.ip:~/.ssh/
```

将文件导入后，接下来就是用新的`.pem`生成新的public key

``` bash
chmod 400 ~/.ssh/aws-new.pem
ssh-keygen -y
```

按提示输入`/home/ubuntu/.ssh/aws-new.pem`，之后可以得到公钥，最后一步就是将新的公钥复制进`~/.ssh/authorized_keys`.复制之前可以先将改文件清空，以清除旧的公钥。

到此就完成了秘钥替换，然后可以退出ssh，用新的`aws-new.pem`重新登录。

refer: [AWS 更换 EC2 密钥](https://blog.csdn.net/gejian1208/article/details/88394691)

## 注意事项

我用的是一年内免费使用的`ec2`套餐，需绑定信用卡，据说到期后`AWS`会自动扣费，所以一定要提前关闭账户！！！此外，平常操作时也要注意各项配置，可能不小心会引入新的扣费功能。
