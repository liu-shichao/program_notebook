总结一下linux搜索so的文件路径顺序

1.linux不会搜索当前文件夹

2.首先搜索/lib和/usr/lib，android搜索/system/lib

3.搜索ld.so.conf中指定的绝对路径

4.搜索LD_LIBRARY_PATH环境变量指定的路径，例如：``export LD_LIBRARY_PATH=./``搜索当前文件夹，这个在android也适用
