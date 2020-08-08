# cmake+NDK命令行编译cpp

1.cmake-toolchains
官网： https://cmake.org/cmake/help/latest/manual/cmake-toolchains.7.html

### 简介
cmake调用用一系列的工具（工具链），来进行代码的编译，库的链接，以及最后的大包生成。在执行主机编译时（在电脑上编译本机运行的程序），cmake会根据CMakeLists.txt中指定的工程语言（后边会介绍如何制定工程的语言），自动识别本机中可用的工具链，进行构建程序，当为其他设备（例如手机或者开发板）编译程序时，需要提供一个工具链文件的信息，用指定的工具链来进行构建程序，也就是交叉编译。

### 在CMakeLists.txt中指定工程使用的语言，通过 ``project(xxxx)`` 命令指定语言，如果顶层的CMakeLists.txt中没有指定``project(xxxx)``命令，会自动生成一个，默认使能了c语言和cxx语言

这样只指定c语言
···
project(C_Only C)
···

这样是不指定任何语言
```
project(MyProject NONE)
```

可以通过之后使用enable_language命令单独开启语言选项
```
enable_language(CXX)
```
当指定语言后，cmake会自动寻找这种指定语言的编译器，并且设置一些信息，例如编译器的厂家和版本，构建目标的cpu的架构和位宽，以及相关构建工具的位置。

``ENABLED_LANGUAGES ``这个全局变量存储了当前指定的语言

### 变量和属性

 CMAKE_<LANG>_COMPILER 是指定语言<LANG>的编译器的完整路径
  
### 交叉编译

在命令行执行cmake命令时，如果指定了``-DCMAKE_TOOLCHAIN_FILE=path/to/file``参数，这个file文件将被提前加载，来指定编译器的参数，并且``CMAKE_CROSSCOMPILING``这个参数会被设置为``true``，说明当前配置为交叉编译模式


2.
