# Git

<!-- toc -->

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
git config --global http.proxy http://127.0.0.1:3128
git config --global https.proxy http://127.0.0.1:3128
```

某些特殊情况下，电脑如何通过ssh访问远程仓库，此时需要使用https，但是默认每次都要重新输入用户名和密码，此时可以配置`credential.helper`为`store`,这样只需要需要一次，本地就会保存相应的证书信息，下次就无需输入了。

``` bash
git config --global credential.helper store
```

## 生成秘钥

为了在远程仓库托管本地代码，首先需要通过keygen生成一组秘钥，并添加至远程代码托管平台。

``` bash
cd
ssh-keygen
cat .ssh/id_rsa.pub
```

添加秘钥至远程仓库，如`github`，`coding`。可以打开远程仓库所在官网，登录个人账户，在**设置**中添加`ssh-key`。

对于没有GUI界面的远程服务器，添加ssh秘钥时可以使用以下指令:

``` bash
ssh-copy-id -i ~/.ssh/id_rsa.pub <username>@<servername>
```

添加完成后，为检验与远程服务器的连接情况，可使用以下指令：

``` bash
$ ssh -T git@github.com
Hi Litreily! You've successfully authenticated, but GitHub does not provide shell access.
```

以`github`为例，以上显示结果表明与`github`能够正常连接。

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
git add -i # 交互式添加，可以添加某个文件的局部修改
```

### git rm

``` bash
git rm <file-name1> <file-name2> ...  # 从暂存区或本地仓库中删除文件，工作区也将其删除
git rm -r --cached <dir-name>/<file-name>  # 将文件或文件夹从暂存区或本地仓库中删除
```

**说明:**如果先通过`add`或`commit`对某些文件或文件夹进行了追踪，当我们在`.gitignore`文件中添加这些文件或文件夹时将不生效，因为忽略文件仅对未跟踪的文件或文件夹生效，为解决这个问题，可以先用`git rm -r --cached`指令移除这些文件或文件夹，以解开对它们的追踪，然后再修改`.gitignore`.

### git mv

``` bash
git mv # 重命名某文件
```

### git commit

``` bash
git commit -m <message>  # 提交暂存区的文件至本地仓库
git commit -a  # 添加修改后文件及新创建的文件，并将这些文件提交至本地仓库
git commit -e  # 提交前编辑提交信息，第一行作为提交主题，空一行后的信息将显示在补丁邮件中
git commit -s  # 提交时使用提交者的签名(Signed-of-by)
git commit -v  # 提交时显示详细的修改信息
git commit --amend  # 修改最新一次提交信息，并重新提交
```

### git push/pull/fetch

``` bash
git push <remote-name> <branch-name>  # 将本地当前分支提交到远程仓库指定分支
git pull <remote-name> <branch-name>  # 从远程仓库指定分支拉取文件至本地，更新本地，可能引起冲突
git fetch <remote-name> <branch-name>  # 从远程仓库指定分支拉取文件至本地缓存文件中

git push -f  # 当某次错误提交至远程仓库时，先在本地撤销(git reset)，之后用改指令强制修改回退远程提交
git push --tags # 提交时将tag一并提交, 注意这将提交所有不在remote的tags
git push <remote-name> <tag-name> # 提交某一个指定tag
git push <remote-name> :refs/tags/<tag-name> # 删除指定的远程tag
```

### git log

``` bash
git log  # 显示简略的提交记录
git log --stat  # 显示每次提交记录的详细信息
git log --pretty=oneline  # 每行显示完整commit ID
```

### git reflog

``` bash
git reflog  # reference logs, 在不小心git reset --hard情况下可以保命
git reflog --oneline
```

### git status

``` bash
git status  # 查看当前本地工作区、暂存区文件的状态
```

### git blame

``` bash
git blame <path/of/file>  # 查看某个文件每行的最新提交记录
```

### git tag

``` bash
git tag  # 列出本地tag
git tag <tag-name> <commit-id>  # 为某次提交添加标签
git tag -d <tag-name>  # 删除本地tag
```

## 合并

### git merge

Join two or more development histories together

``` bash
current branch: master

      A---B---C topic
     /
D---E---F---G master

$ git merge topic

      A---B---C topic
     /         \
D---E---F---G---H master
```

### git rebase

Reapply commits on top of another base tip

``` bash
git rebase -i # interactive
```

``` bash
current branch: topic

      A---B---C topic
     /
D---E---F---G master

$ git rebase master
$ git rebase master topic

              A'--B'--C' topic
             /
D---E---F---G master
```

### git cherry-pick

Apply the changes introduced by some existing commits

``` bash
git cherry-pick <commit>
```

## 暂存

### git stash

``` sh
➜  Notes git:(master) git stash
apply         -- apply the changes recorded in the stash
branch        -- branch off at the commit at which the stash was originally created
clear         -- remove all the stashed states
create        -- create a stash without storing it in the ref namespace
drop          -- remove a single stashed state from the stash list
list          -- list the stashes that you currently have
pop           -- remove and apply a single stashed state from the stash list
save    push  -- save your local modifications to a new stash
show          -- show the changes recorded in the stash as a diff
```

## 添加子模块

### git submodule add

``` sh
git submodule add <repo.git>
```

``` sh
➜  Python-demos git:(master) ✗ git submodule add git@github.com:Litreily/Gitbook2HexoDoc.git
Cloning into '/home/litreily/workspace/Python-demos/Gitbook2HexoDoc'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 15 (delta 3), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (15/15), 5.87 KiB | 5.87 MiB/s, done.
Resolving deltas: 100% (3/3), done.
➜  Python-demos git:(master) ✗ gst
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

          new file:   .gitmodules
          new file:   Gitbook2HexoDoc
```

首次添加子项目会多出一个`.gitmodules`文件,用于存储子项目的基本信息. 默认情况下新添加的子项目及`.gitmodules`都会存入暂存区, 此时通常需要`commit`一次.

## 撤销操作

### git reset

``` bash
git reset <commit-id> # 撤销最新提交至commit-id间所有内容
git reset HEAD~n  # 撤销前n次提交

# 撤销方式
git reset --soft  # 仅删除本地仓库修改，保留修改值暂存区
git reset --mixed # 默认方式，删除暂存区及本地仓库修改，将撤销包含的修改移至工作区
git reset --hard  # 删除工作区，暂存区及本地仓库所有修改

# before reset：
# ----0----1----2----3----4(HEAD)
# git reset commit 2
# after reset：
# ----0----1----2(HEAD)
```

### git revert

``` bash
git revert <commit-id>  # 撤销指定的某次提交，被撤销的提交记录保留在历史记录中，同时生成一个新的提交记录

# before revert：
# ----0----1----2----3----4(HEAD)
# git revert commit 2
# after revert：
# ----0----1----2----3----4---<revert-commit-of-2>(HEAD)
```

## 补丁操作

### git format-patch

将修改的代码写入补丁文件中

``` bash
git format-patch -n <commit-id>  # 将前n次提交的commit内容写入补丁
git format-patch HEAD^^^  # 补丁个数与'^'个数相同，从最近一次往前计数
git format-patch HEAD~n  # 补丁个数等于n，从最近一次往前计数
```

### git am

将补丁文件应用到某仓库中

``` bash
git am -s <patches-name>  # 打单个或多个补丁到某个仓库，-s用于签名
git am -i <patches-name>  # 交互式应用patch，可以手动修改patch的提交信息
git am -s --reject <patches-name>  # 打补丁时显示冲突，方面定位到有冲突的地方
git am --abort  # 终止当前am操作，通常在打补丁失败时执行
```

### git send-email

将补丁以邮件形式发送出去

``` bash
git send-email --to <username@email> --smtp-server <server-address> <patchs-name> # 通过邮件发送补丁
```

如果需要取消CC patch中signed-off-by的相关人员，可以将sendemail.suppresscc配置为all. 与`send-email`相关的常用配置如下：

``` bash
git config --global sendemail.suppresscc all
git config --global sendemail.smtpserver <smtpserver>
git config --global sendemail.confirm always
```

## 其它指令

### gitk

打开git的图形化界面

### tig

Linux服务器端的利器，`git`的文本模式接口

``` bash
tig
tig show  # 查看最新一次的提交
tig status  # 与git status类似

tig </path/of/file/or/dir>  # 查看某文件或目录的提交记录
tig blame </path/of/file>  # 查看某文件最新一次修改记录

tig <commit-id>  # 指定某次commit-id
tig <branch-name>  # 指定某个分支
tig <tag-name>  # 指定某个标签

# 说明：可以在指定分支时同时指定文件或目录
```
