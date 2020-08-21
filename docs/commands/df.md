# df

> report file system disk space usage

## usage

``` zsh
➜  df -<TAB>
--all             -a  -- include dummy file systems
--block-size      -B  -- specify block size
--exclude-type    -x  -- exclude file systems of specified type
--help                -- display help and exit
--human-readable  -h  -- print sizes in human readable format
--inodes          -i  -- list inode information instead of block usage
-k                    -- like --block-size=1K
--local           -l  -- limit listing to local file systems
--no-sync             -- do not invoke sync before getting usage info (default)
--portability     -P  -- use the POSIX output format
--print-type      -T  -- print file system type
--si              -H  -- human readable fomat, but use powers of 1000 not 1024
--sync                -- invoke sync before getting usage info
--total               -- produce a grand total
--type            -t  -- limit listing to file systems of specified type
-v                    -- (ignored)
--version             -- output version information and exit
```

## examples

``` bash
df # 默认以KB为单位
df -a # 显示所有，包含伪文件系统、文件系统副本和不可访问的文件系统
df -h # 方便人类可读 (1K = 1024)
df -H # 方便人类可读 (1K = 1000)
df -i # 显示inode
df -BM # 以MB为单位，M可替换为K,M,G,T,P,E,Z,Y
```
