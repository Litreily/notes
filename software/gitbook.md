# Gitbook

<!-- toc -->

## 安装Gitbook

在安装 `node.js` 前提下，输入

``` bash
npm install -g gitbook-cli
gitbook -V
```

## 常用指令

``` bash
gitbook init  # 初始化文件目录	
gitbook serve  # 生成静态网页，并打开本地服务器localhost:4000
gitbook build  # 生成静态网页，并存入_book文件夹
gitbook --help  # 显示与gitbook相关的指令
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

## book.json

``` json
{
    "title" : "Notes",
    "author": "litreily",
    "description": "Log importants things of my work and my life",
    "links" : {
        "sidebar" : {
            "Home"  : "http://www.litreily.top",
            "smslit's notes": "https://www.smslit.top/notebook/"
        }
    },

    "styles": {
        "website": "styles/website.css"
    },

    "plugins": [
        "toggle-chapters",
        "etoc",
        "github"
    ],
    "pluginsConfig": {
        "etoc": {
            "h2lb": 3,
            "mindepth": 2,
            "maxdepth": 4,
            "notoc": false
        },
        "github": {
            "url": "https://github.com/Litreily/Notes"
        }
    }
}
```
