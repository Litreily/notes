# powershell

## 添加配置文件`PROFILE`

打开`Powershell`，输入指令：

``` bash
mkdir C:\<username>\Documents\WindowPowerShell\Microsoft.PowerShell_profile.ps1
$PROFILE="C:\<username>\Documents\WindowPowerShell\Microsoft.PowerShell_profile.ps1"
```

`PowerShell`每次启动都会读取配置文件`$PROFILE`中的内容，类似于`Linux`中的`.profile`和`.bashrc`.

## 添加`alias`

和`bash`一样，`PowerShell`同样可以配置别名

``` bash
Set-Alias <name> <value>  # 添加alias，不区分大小写
Set-Item alias:<name> <value>  # 功能与Set-Alias一致
Remove-Item alias:<name>  # 删除alias
```

值得注意的是，如果在命令行中添加`alias`，那么在下一次启动后就会失效，为了保证添加的`alias`永久有效，可以将其写入`$PROFILE`文件中。下次启动`PowerShell`时，它将自动获取文件中的别名并令其生效。

## 添加函数

``` bash
funciton <name> {content}
```

函数同样可以放置在`$PROFILE`中。
