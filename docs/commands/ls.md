# ls

> list directory contents

## usage

``` zsh
➜  ls -<TAB>
-1                        -- single column output
--all                 -a  -- list entries starting with .
--almost-all          -A  -- list all except . and ..
--author                  -- print the author of each file
--block-size              -- specify block size
-c                        -- status change time
-C                        -- list entries in columns sorted vertically
--classify            -F  -- append file type indicators
--dereference         -L  -- list referenced file for sym link
--directory           -d  -- list directory entries instead of contents
--dired               -D  -- generate output designed for Emacs' dired mode
--escape              -b  -- print octal escapes for control characters
-f                        -- unsorted, all, short list
--file-type           -p  -- append file type indicators except *
--full-time               -- list both full date and full time
-g                        -- long listing but without owner information
--help                    -- display help information
--hide-control-chars  -q  -- hide control chars
--human-readable      -h  -- print sizes in human readable form
--ignore              -I  -- don't list entire matching pattern
--ignore-backups      -B  -- don't list entries ending with ~
--inode               -i  -- print file inode numbers
--kilobytes           -k  -- use block size of 1k
-l                        -- long listing
--literal             -N  -- print raw characters
-m                        -- comma separated
--no-group            -G  -- inhibit display of group information
--numeric-uid-gid     -n  -- numeric uid, gid
-o                        -- no group, long
--quote-name          -Q  -- quote names
--recursive           -R  -- list subdirectories recursively
--reverse             -r  -- reverse sort order
-S                        -- sort by size
--si                  -H  -- sizes in human readable form; powers of 1000
--size                -s  -- display size of each file in blocks
-t                        -- sort by modification time
--tabsize             -T  -- specify tab size
--time                    -- specify time to show
--time-style              -- show times using specified style
-u                        -- access time
-U                        -- unsorted
-v                        -- sort by version (filename treated numerically)
--version                 -- display version information
--width               -w  -- specify screen width
-x                        -- sort horizontally
-X                        -- sort by extension
--dereference-command-line
--dereference-command-line-symlink-to-dir
--format
--indicator-style
--quoting-style
--show-control-chars
--sort
```

## examples

``` bash
ls # 显示当前路径下的文件及文件夹
ls -a # 显示所有文件（包含隐藏文件及文件夹）
ls -F # 在目录后显示'\'，在可执行文件后显示‘*’，便于区分文件及文件夹
ls -l # 以长列表形式显示文件的详细信息
ls -R # 递归显示文件和文件夹，以及子目录的文件及文件夹
ls -r # 逆序显示
ls -s # 显示大小
ls -sh # 显示大小和单位
ls -i # 显示inode
ls -1 # 一行显示一条记录
```
