# du

> Disk Usage

## usage

``` zsh
➜  du -<TAB>
--all               -a      -- write counts for all files
--apparent-size             -- print apparent sizes rather than disc usage
--block-size        -B      -- specify block size
--bytes             -b      -- equivalent to --apparent-size --block-size=1
--count-links       -l      -- count sizes many times if hard linked
--dereference       -L      -- dereference all symlinks
--dereference-args  -D  -H  -- dereference arguments that are symlinks
--exclude                   -- exclude files matching pattern
--exclude-from      -X      -- exclude files matching any pattern in file
--files0-from               -- use NUL-terminated list of files from file
--help                      -- display help information
--human-readable    -h      -- print sizes in human readable format
-k                          -- use block size of 1k
-m                          -- use block size of 1M
--max-depth                 -- maximum levels to recurse
--no-dereference    -P      -- do not dereference any symlinks
--null              -0      -- end each output line with NUL instead of newline
--one-file-system   -x      -- skip directories on different filesystems
--separate-dirs     -S      -- do not include size of subdirectories
--si                        -- human readable form using powers of 1000
--summarize         -s      -- only report total for each argument
--threshold         -t      -- report only entries for which size exceeds threshold
--time                      -- show time of last modification of any file in the directory
--time-style                -- show times using given style, +FORMAT for strftime formatted args
--total             -c      -- produce a grand total
--version                   -- display version information
```

## examples

``` bash
du # 显示当前目录所有文件大小明细
du -s # 显示当前目录总占用空间
du -h # 显示当前目录所有文件大小明细，显示单位
du -sh # 查看当前目录占用空间，显示单位
```
