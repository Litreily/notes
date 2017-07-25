## 全局配置

配置全局参数的指令如下：

``` bash
git config --global <global-name> <global-value>
git config -l  # 查看git的全局配置信息
```

常用的全局变量有`user.name`,`user.email`,`core.editor`

``` bash
git config --global user.name litreily
git config --global user.email litreily@outlook.com
git config --global core.editor vim
```

## 生成秘钥

为了在远程仓库托管本地代码，首先需要通过keygen生成一组秘钥，并添加至远程代码托管平台。

``` bash
cd
ssh-keygen
cat .ssh/id_rsa.pub
```

对于没有GUI界面的远程服务器，添加ssh秘钥时可以使用以下指令:

``` bash
ssh-copy-id -i ~/.ssh/id_rsa.pub <username>@<servername>
```

## 远程操作

### git remote

``` bash
git remote add <remote-name> <remote-address>  # 添加远程路径（ssh,http,...）
git remote -v  # 显示当前所有远程路径的详细信息
```

### git clone

``` bash
git clone <remote-address>  # 从远程仓库克隆项目文件至本地
```

## 常用指令

### git add

``` bash
git add .  # 添加所有修改后的文件和新创建的文件至暂存区（staging area)
git add <file-name1> <file-name2> ...  # 添加指定文件至暂存区（staging area）
```

### git commit

``` bash
git commit -m <message>  # 提交暂存区的文件至本地仓库
git commit -a  # 添加修改后文件及新创建的文件，并将这些文件提交至本地仓库
git commit -e  # 提交前编辑提交信息，第一行作为提交主题，空一行后的信息将显示在补丁邮件中
```

### git push/pull/fetch

``` bash
git push <remote-name> <branch-name>  # 将本地当前分支提交到远程仓库指定分支
git pull <remote-name> <branch-name>  # 从远程仓库指定分支拉取文件至本地，更新本地，可能引起冲突
git fetch <remote-name> <branch-name>  # 从远程仓库指定分支拉取文件至本地缓存文件中
```

### git log

``` bash
git log  # 显示简略的提交记录
git log --stat  # 显示每次提交记录的详细信息
git log --pretty=oneline  # 每行显示完整commit ID
```

### git status

``` bash
git status  # 查看当前本地工作区、暂存区文件的状态
```

### git tag

``` bash
git tag <tag-name> <commit-id>  # 为某次提交添加标签
```

## 打补丁并发送邮件

### git format-patch/send-email

将修改的代码写入补丁文件中

``` bash
git format-patch -n <numer>  # 将前n次提交的commit内容写入补丁
git format-patch HEAD^^^  # 补丁个数与'^'个数相同，从最近一次往前计数
```

将补丁以邮件形式发送出去

``` bash
git send-email --to <username@email> --smtp-server <server-address> <patchs-name> # 通过邮件发送补丁
```

## 其它指令

### gitk

打开git的图形化界面




