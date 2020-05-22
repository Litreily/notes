# CSS

## 自定义滚动条

仅支持Chrome浏览器

``` css
::-webkit-scrollbar {
  width: 5px;
  height: 5px;
}

::-webkit-scrollbar-thumb {
  border-radius: 3px;
  background-color: #888;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #ccc;
}
```

## 绘制三角形

在div(以article为例)添加`:before`元素，使用绝对位置，通过设置border样式实现三角形

``` css
article:before {
  content: "";
  position: absolute;
  top: -12px;
  left: 0;
  border-color: transparent #16212b #16212b transparent;
  border-style: solid;
  border-width: 6px 20px;
  width: 0;
  height: 0;
}
```

## 添加主题颜色

在网页中添加元标签`theme-color`，设置主题颜色后，手机浏览器可以依据主题颜色修改浏览器外观颜色。

```html
<meta name="theme-color" content="#2d4356">
```
