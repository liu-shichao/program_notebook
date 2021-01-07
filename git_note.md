### 4.git将当前修改的内容移动到别的分支

方法1. 当前的修改不要提交，然后新建一个分支，切换到新分支的时候会发现这些修改的内容都被带过来了，再切换回原来分支查看修改还在，这是两个分支都有这些修改，然后再切换到新的分支进行提交，这时候原来的分支就看不见这些修改了。

方法2.用stash命令，将当前的分支修改内容暂存起来，然后切换到其他分支，再执行git stash pop， 就可以将这些修改加到其他分支了。



### 3.git删除子模块

OtherLibrary/MKStore是子模块的文件夹路径，相对于跟路径，执行这个命令不会删除已有的代码文件，只会删除子模块标记

```
git rm --cached OtherLibrary/MKStore
```


### 2.git中提交空文件

git中是不跟踪空文件的，所以``git add .``之后并不会将空文件夹加入到缓存区，如果需要提交一个空目录需要再空目录中新建一个``.gitkeep``文件，内容可以为空，这样再add然后commit就会有了。


### 1.git 中的文件模式代码的含义

参考：
1. https://github.com/git/git/blob/e67fbf927dfdf13d0b21dc6ea15dc3c7ef448ea0/Documentation/technical/index-format.txt#L65
2. https://stackoverflow.com/a/8347325

```
Also, a directory object type (binary 0100) and group-writeable (0664 permissions) regular file are allowed as indicated by the fsck.c fsck_tree method. The regular non-executable group-writeable file is a non-standard mode that was supported in earlier versions of Git.

This makes valid modes (as binary and octal):

0100000000000000 (040000): Directory
1000000110100100 (100644): Regular non-executable file
1000000110110100 (100664): Regular non-executable group-writeable file
1000000111101101 (100755): Regular executable file
1010000000000000 (120000): Symbolic link
1110000000000000 (160000): Gitlink
```
