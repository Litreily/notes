# mksquashfs

> mksquashfs - tool to create and append to squashfs filesystems

`squashfs`是linux中一个高度压缩的只读文件系统，使用zlib压缩文件、INode以及目录，通常用于归档。

## usage

``` zsh
mksquashfs SOURCE [SOURCE2 ...] DESTINATION [OPTIONS]
```

``` zsh
➜  mksquashfs -h
SYNTAX:mksquashfs source1 source2 ...  dest [options] [-e list of exclude
dirs/files]

Filesystem build options:
-comp <comp>            select <comp> compression
                        Compressors available:
                                gzip (default)
                                lzma
                                lzo
                                lz4
                                xz
-b <block_size>         set data block to <block_size>.  Default 128 Kbytes
                        Optionally a suffix of K or M can be given to specify
                        Kbytes or Mbytes respectively
-no-exports             don't make the filesystem exportable via NFS
-no-sparse              don't detect sparse files
-no-xattrs              don't store extended attributes
-xattrs                 store extended attributes (default)
-noI                    do not compress inode table
-noD                    do not compress data blocks
-noF                    do not compress fragment blocks
-noX                    do not compress extended attributes
-no-fragments           do not use fragments
-always-use-fragments   use fragment blocks for files larger than block size
-no-duplicates          do not perform duplicate checking
-all-root               make all files owned by root
-force-uid uid          set all file uids to uid
-force-gid gid          set all file gids to gid
-nopad                  do not pad filesystem to a multiple of 4K
-keep-as-directory      if one source directory is specified, create a root
                        directory containing that directory, rather than the
                        contents of the directory
-fstime secs            Set fs time to seconds since epoch.  Default to current time

Filesystem filter options:
-p <pseudo-definition>  Add pseudo file definition
-pf <pseudo-file>       Add list of pseudo file definitions
-sort <sort_file>       sort files according to priorities in <sort_file>.  One
                        file or dir with priority per line.  Priority -32768 to
                        32767, default priority 0
-ef <exclude_file>      list of exclude dirs/files.  One per line
-wildcards              Allow extended shell wildcards (globbing) to be used in
                        exclude dirs/files
-regex                  Allow POSIX regular expressions to be used in exclude
                        dirs/files

Filesystem append options:
-noappend               do not append to existing filesystem
-root-becomes <name>    when appending source files/directories, make the
                        original root become a subdirectory in the new root
                        called <name>, rather than adding the new source items
                        to the original root

Mksquashfs runtime options:
-version                print version, licence and copyright message
-exit-on-error          treat normally ignored errors as fatal
-recover <name>         recover filesystem data using recovery file <name>
-no-recovery            don't generate a recovery file
-info                   print files written to filesystem
-no-progress            don't display the progress bar
-progress               display progress bar when using the -info option
-processors <number>    Use <number> processors.  By default will use number of
                        processors available
-mem <size>             Use <size> physical memory.  Currently set to 1488M
                        Optionally a suffix of K, M or G can be given to specify
                        Kbytes, Mbytes or Gbytes respectively

Miscellaneous options:
-root-owned             alternative name for -all-root
-noInodeCompression     alternative name for -noI
-noDataCompression      alternative name for -noD
-noFragmentCompression  alternative name for -noF
-noXattrCompression     alternative name for -noX

-Xhelp                  print compressor options for selected compressor

Compressors available and compressor specific options:
        gzip (default)
          -Xcompression-level <compression-level>
                <compression-level> should be 1 .. 9 (default 9)
          -Xwindow-size <window-size>
                <window-size> should be 8 .. 15 (default 15)
          -Xstrategy strategy1,strategy2,...,strategyN
                Compress using strategy1,strategy2,...,strategyN in turn
                and choose the best compression.
                Available strategies: default, filtered, huffman_only,
                run_length_encoded and fixed
        lzma (no options)
        lzo
          -Xalgorithm <algorithm>
                Where <algorithm> is one of:
                        lzo1x_1
                        lzo1x_1_11
                        lzo1x_1_12
                        lzo1x_1_15
                        lzo1x_999 (default)
          -Xcompression-level <compression-level>
                <compression-level> should be 1 .. 9 (default 8)
                Only applies to lzo1x_999 algorithm
        lz4
          -Xhc
                Compress using LZ4 High Compression
        xz
          -Xbcj filter1,filter2,...,filterN
                Compress using filter1,filter2,...,filterN in turn
                (in addition to no filter), and choose the best compression.
                Available filters: x86, arm, armthumb, powerpc, sparc, ia64
          -Xdict-size <dict-size>
                Use <dict-size> as the XZ dictionary size.  The dictionary size
                can be specified as a percentage of the block size, or as an
                absolute value.  The dictionary size must be less than or equal
                to the block size and 8192 bytes or larger.  It must also be
                storable in the xz header as either 2^n or as 2^n+2^(n+1).
                Example dict-sizes are 75%, 50%, 37.5%, 25%, or 32K, 16K, 8K
                etc.
```

## examples

``` zsh
# 使用xz压缩算法，1个处理器
mksquashfs source/ source-xz.squashfs -comp xz -processors 1
```

