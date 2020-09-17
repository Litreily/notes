# rsync

## usage

```bash
rsync -r source destination
```

## examples

### local rsync

```bash
rsync -a ~/blog/source /mnt/e/workspace/blog
```

### remote rsync

```bash
rsync -a source/ username@remote_host:destination
rsync -a username@remote_host:source/ destination
```

rsync默认使用ssh协议连接远程服务器，如果有额外参数，比如非默认端口，则需要使用`-e`

```bash
rsync -av -e 'ssh -p 1234' source/ username@remote_host:/destination
```

## reference

- [阮一峰 - rsync 用法教程](http://www.ruanyifeng.com/blog/2020/08/rsync.html)