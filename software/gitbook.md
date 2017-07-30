## 安装Gitbook

在安装 `node.js` 前提下，输入
``` bash
npm install -g gitbook-cli
gitbook -V
```

## 添加配置文件

``` bash
vim book.json
```

## 安装插件

首先在`book.json`中添加插件信息，以`toggle-chapters`插件为例：

``` json
{
    "plugins": ["toggle-chapters"]
}
```

然后执行`gitbook install`指令安装插件。

