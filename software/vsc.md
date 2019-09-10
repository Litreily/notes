# Visual Studio Code

## 常用快捷键

* 指令窗口：`Ctrl+Shift+P`
* 最近文件：`Ctrl+P`
* 选择所有与当前所在单词相同的单词：`Ctrl+F2`
* 选择所有与当前所选内容相同的字符串：`Ctrl+Shift+L`

* 快捷键列表：<https://code.visualstudio.com/shortcuts/keyboard-shortcuts-linux.pdf>

## extensions

* Color Theme
  * Dark(Visual Studio)
  * Solarized Dark
  * One Dark Pro
* File Icon Theme
  * VSCode Great Icons
  * Material Icon Theme
* Remote - WSL
* Python
* Git
  * GitLens
  * Git History

## 常用配置

### 设置分界线

在`settings.json`文件中添加`editor.rulers`，数组每一个数对应一条线。

``` json
"editor.rulers": [80,120],
```

### code format

使用`Shift Alt F`可以自动格式化代码，针对`python`代码，会提示需要安装`autopep8`，可以通过`VSCode`的弹框信息安装，也可以手动安装

``` bash
pip install --upgrade autopep8
```

### python related

每次执行python代码时，总是会弹出新的`terminal`，此时可以通过配置`launch.json`解决这个问题

``` json
"console": "integratedTerminal",
```

references:

* [(Ctrl + ) F5 opening new terminal everytime #56341](https://github.com/Microsoft/vscode/issues/56341)
* [Debug Launch Configuration: Add a setting to for integrated.terminal path on each configuration or for all python debugging. #2391](https://github.com/microsoft/vscode-python/issues/2391)

~~PS：我的多台PC的多个系统都装有`VSCode`和`python`插件，但并不是所有系统都有这个问题。~~

PS again: 后经观察，发现在使用`git bash`时才有这个问题，如果使用`CMD`作为默认终端则没有这个问题。
