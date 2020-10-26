### 1.使用lldb加载要被调试的程序

```
lldb xxx.app
```

例如:

```
lldb ~/build-untitled1-Desktop_Qt_5_12_0_clang_64bit-Debug/untitled1.app
```

### 2.设置断点

```
breakpoint set --file xxx.cpp --line xx
```

例如：

```
breakpoint set --file mainwindow.cpp --line 17
```

### 3.运行程序

```
run
```

### 4.查看变量

xxx为要查看的变量名

```
frame variable xxx
```

### 5.单步运行

```
step-over
```

### 6.全速运行

```
process continue
```

