# Shell

<!-- toc -->

## 配置

### 配置 bash

``` bash
vim ~/.bashrc
source .bashrc  # 记得使用source指令，否则更新内容无法生效
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

### 配置grub开机顺序

1. 修改`/boot/grub/grub.cfg`
2. 修改`/etc/default/grub`并执行`update-grub2` [推荐]
