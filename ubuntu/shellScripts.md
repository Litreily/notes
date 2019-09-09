
# Shell scripts

<!-- toc -->

## 自动更新gitbook电子书

push.sh

``` bash
#!/bin/zsh

git add .
git commit -m "update notes"
git push

# notes: exec cmd "chmod u+x push.sh" before "./push.sh"
```

当更新完`Notes`后，执行`./push.sh`可以自动完成代码提交和上传的操作，执行结束后，远程`github`仓库文件将会更新，与`github`绑定的`gitbook`自动获取更新内容，进而更新电子书所在站点的内容。

## 自动更新个人博客

push.sh

``` bash
#!/bin/zsh

# push all the changed files and untracked files of blog
git add .
git commit -m "update blog files"
git push

# generate website files and deploy it to www.litreily.top
hexo clean
hexo g -d
```

执行`./push.sh`可以自动完成博客网站的更新。
