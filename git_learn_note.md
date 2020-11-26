
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
