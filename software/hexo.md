### 安装 Hexo
使用 `node.js` 中的包管理工具 `npm` 安装 `hexo`

``` bash
npm install hexo-cli -g
hexo init <blog-floder-name>  # e.g. Blog
cd <blog-floder-name>
npm install
```

### 常用插件
``` bash
npm install hexo-server --save
npm install hexo-deployer-git --save

npm install hexo-generator-tag --save
npm install hexo-generator-archive --save
npm install hexo-generator-category --save
npm install hexo-generator-feed --save
npm install hexo-generator-sitemap --save
npm install hexo-generator-index --save
npm install hexo-generator-search --save

npm install hexo-renderer-jade --save
npm install hexo-renderer-ejs --save
npm install hexo-renderer-less --save
npm install hexo-renderer-sass --save
npm install hexo-renderer-stylus --save
npm insatll hexo-renderer-marked --save
```

### 分页功能

在保证`hexo-generator-index`,`hexo-generator-tag`,`hexo-generator-archive`已安装的情况下，可以通过修改博客根目录下的`_config.yml`文件令主页、归档页与标签页使用不同的`per_page`，保证不同页面的每页内容列表数不相同。

``` yml
index_generator:
  per_page: 8

archive_generator:
  per_page: 0
  yearly: true
  monthly: false

tag_generator:
  per_page: 0
```

当`per_page`为0时，代表不分页。