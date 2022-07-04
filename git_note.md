### 11.git强制添加被ignore忽略的文件
```
git add -f App.class
```

### 10.gitk 可视化工具

```
显示全部分支的提交记录（本地分支 + 远程分支）
gitk --all
```


### 9.git log --oneline --all --graph -n4

```
--oneline log采用一行的方式显示

--all 显示所有的分支的历史提交

--graph  采用图形的方式显示分支结构

--n4 显示最近的4条历史记录

```

### 8.git mv xx xx
重命名的方法，可以直接commit

### 7.git add -u

```
git add -u 
将已经被管理的文件的变动添加到暂存区
```

### 6.git子模块的添加

1.添加，其中url是git的网址，path是新建的文件夹的相对git的根目录的路径。
```
git submodule add url path
```
2.提交
```
git commit -m "xxx"
```


### 5.git误提交到HEAD detached分支，切换其他分支后导致代码丢失的解决办法
问题描述：1.没有注意当前处于HEAD detached分支，将代码都提交到了这个分支上，当切换回master分支后，提交记录都不见了，解决方法如下。

解决方法：

1. 执行 ``git reflog``，能够查看到HEAD detached分支的提交名字,示例如下
```
liushichao@ShichaodeMacBook-Pro core % git reflog    
8e310b4 (HEAD -> master, origin/master, origin/HEAD) HEAD@{0}: checkout: moving from 1017f1ee6ce9a434a723de9c2ad4e52eabca267e to master
1017f1e HEAD@{1}: commit: 插值模块增加速度参数
be3959d HEAD@{2}: commit: 修改速度为参数传递字符串
8e310b4 (HEAD -> master, origin/master, origin/HEAD) HEAD@{3}: checkout: moving from 01b0d7489a80548c63021b050bddfaedee304481 to 8e310b40cd4cee5893b57cab92d412002d7cd23b
01b0d74 HEAD@{4}: commit: 传递gps相关信息
8e310b4 (HEAD -> master, origin/master, origin/HEAD) HEAD@{5}: checkout: moving from 278f1f051f41e5d08ab87b2092411462e2becd5d to 8e310b40cd4cee5893b57cab92d412002d7cd23b
278f1f0 HEAD@{6}: checkout: moving from master to 278f1f051f41e5d08ab87b2092411462e2becd5d
8e310b4 (HEAD -> master, origin/master, origin/HEAD) HEAD@{7}: commit: 增加实例化对象索引id,用来查找最后一帧缓存的图像
278f1f0 HEAD@{8}: checkout: moving from a150b66d85a6f0b26cc21c2013002c62ffe6170c to master
a150b66 HEAD@{9}: checkout: moving from master to a150b66d85a6f0b26cc21c2013002c62ffe6170c
278f1f0 HEAD@{10}: pull origin master: Fast-forward
b30b1c2 HEAD@{11}: pull origin master: Fast-forward
81a731e HEAD@{12}: pull origin master: Fast-forward
a150b66 HEAD@{13}: checkout: moving from 748bb9c1a89f405d47a8136c36527699792aaa82 to master
748bb9c HEAD@{14}: checkout: moving from master to 748bb9c1a89f405d47a8136c36527699792aaa82
a150b66 HEAD@{15}: clone: from https://git.sogou-inc.com/fanyongxing/Mapping_Reconstruction
```
2.切换到最后一次的HEAD提交上 ``git checkout 1017f1e``,示例如下
```
liushichao@ShichaodeMacBook-Pro core % git checkout 1017f1e
Note: switching to '1017f1e'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 1017f1e 插值模块增加速度参数
```

3.现在已经找回丢失的提交了，下边新建一个分支名字叫diff，叫什么名字都行，将这个detached的HEAD分支保存起来，如下

```
liushichao@ShichaodeMacBook-Pro core % git checkout -b diff
Switched to a new branch 'diff'
```

4.最后将这个分支合并到master分支
```
git checkout master

git merge diff
```
5.完成。


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
