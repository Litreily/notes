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
  * vscode-icons
* Remote - WSL
* Vim
* Language
  * Python
  * C/C++
* Git
  * GitLens
  * Git History
  * Github
* Visual
  * Drawio Integration
  * Debug Visualizer
  * HTML Preview
  * hexdump for VSCode
* Markdown
  * Markdown All in One
  * Markdown PDF
  * Markdown Preview Github Styling
  * markdownlint
* Debugger for Chrome
* Apps
  * Zhihu On VSCode
  * LeetCode

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

## 开发环境

### C/C++

1. 安装`C/C++`插件
2. debug C 代码，自动提示配置`launch.json`, `tasks.json`

#### launch.json

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "gcc - Build and debug active file",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "gcc build active file",
            "miDebuggerPath": "/usr/bin/gdb"
        }
    ]
}
```

#### tasks.json

```json
{
    "tasks": [
        {
            "type": "shell",
            "label": "gcc build active file",
            "command": "/usr/bin/gcc",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}/${fileBasenameNoExtension}"
            ],
            "options": {
                "cwd": "/usr/bin"
            }
        }
  ],
  "presentation": {
    "echo": true,
    "reveal": "always",
    "focus": false,
    "panel": "shared",
    "showReuseMessage": true,
    "clear": false
  },
    "version": "2.0.0"
}
```

## Code server

在浏览器访问VPS上部署的VSCode server, 简直不要太棒！

* [code server](https://github.com/cdr/code-server)

### install on ubuntu

```zsh
curl -fsSL https://code-server.dev/install.sh |sh
```

### run

```zsh
systemctl --user enable --now code-server
```

### config

更改配置文件中的密码、端口（默认8080），如果是用vps，需要将配置文件中的`127.0.0.1`替换为`0.0.0.0`，否则打开端口映射也没法访问。

```zsh
vi ~/.config/code-server/config.yaml
systemctl --user restart code-server
```
