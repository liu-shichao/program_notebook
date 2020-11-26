
### 文件权限代码解释

执行 ls -l
出现下列提示：

```
liushichao@computername main_proj % ls -l
total 0
-rw-r--r--  1 liushichao  staff    0 11 26 18:25 CMakelists.txt
drwxr-xr-x  2 liushichao  staff   64 11 26 17:25 include
drwxr-xr-x  5 liushichao  staff  160 11 26 17:49 sgmm-doc
drwxr-xr-x  2 liushichao  staff   64 11 26 17:25 src
```

其中 ``drwxr-xr-x`` 代表文件权限，具体每个字母的含义

理解的时候将后边每三个分成一组

```
d             rwx            r-x                r-x
|             |              |                  |
代表是目录      当前用户权限     当前用户组权限       其他用户权限
```

d代表是目录，如果是文件的话，这个位置为`-``，如第一行所示

```
-rw-r--r--  1 liushichao  staff    0 11 26 18:25 CMakelists.txt
```


其中 ``rwx`` 的含义为

```
r 读权限
w 写权限
x 可执行权限
```
如果某一个权限是``-``，代表没有那个权限

rwx可以用二进制表示，有权限的地方为1，没权限的位置为0

rwx可以表示为111，转换成十进制为7

r--可以表示为100，对应十进制4

--x二进制为001，十进制为1

