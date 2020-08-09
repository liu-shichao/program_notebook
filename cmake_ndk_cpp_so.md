# cmake+NDK命令行编译cpp

#### 注意 不要用[cmake内建的ndk交叉编译](https://cmake.org/cmake/help/latest/manual/cmake-toolchains.7.html#cross-compiling-for-android),因为目前不是android在维护，如果cmake与ndk的版本不匹配很容易编译出错，[出处在这里](https://developer.android.com/ndk/guides/cmake)

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


## 2.android sdk 版本名称
出处：https://developer.android.com/guide/topics/manifest/uses-sdk-element.html


Platform Version	API Level	VERSION_CODE	Notes
Android 10.0	29	Q	Platform Highlights
Android 9	28	P	Platform Highlights
Android 8.1	27	O_MR1	Platform Highlights
Android 8.0	26	O	Platform Highlights
Android 7.1.1
Android 7.1	25	N_MR1	Platform Highlights
Android 7.0	24	N	Platform Highlights
Android 6.0	23	M	Platform Highlights
Android 5.1	22	LOLLIPOP_MR1	Platform Highlights
Android 5.0	21	LOLLIPOP
Android 4.4W	20	KITKAT_WATCH	KitKat for Wearables Only
Android 4.4	19	KITKAT	Platform Highlights
Android 4.3	18	JELLY_BEAN_MR2	Platform Highlights
Android 4.2, 4.2.2	17	JELLY_BEAN_MR1	Platform Highlights
Android 4.1, 4.1.1	16	JELLY_BEAN	Platform Highlights
Android 4.0.3, 4.0.4	15	ICE_CREAM_SANDWICH_MR1	Platform Highlights
Android 4.0, 4.0.1, 4.0.2	14	ICE_CREAM_SANDWICH
Android 3.2	13	HONEYCOMB_MR2	
Android 3.1.x	12	HONEYCOMB_MR1	Platform Highlights
Android 3.0.x	11	HONEYCOMB	Platform Highlights
Android 2.3.4
Android 2.3.3	10	GINGERBREAD_MR1	Platform Highlights
Android 2.3.2
Android 2.3.1
Android 2.3	9	GINGERBREAD
Android 2.2.x	8	FROYO	Platform Highlights
Android 2.1.x	7	ECLAIR_MR1	Platform Highlights
Android 2.0.1	6	ECLAIR_0_1
Android 2.0	5	ECLAIR
Android 1.6	4	DONUT	Platform Highlights
Android 1.5	3	CUPCAKE	Platform Highlights
Android 1.1	2	BASE_1_1	
Android 1.0	1	BASE

### NDK中支持的c++标准库
[ANDROID_STL](https://developer.android.com/ndk/guides/cmake#android_stl)
NDK r18以前可以使用gnustl标准库
r18开始去掉了gnustl标准库，只有libc++,支持动态库c++_shared 或者静态库c++_static，对应的文件为libc++_shared.so和libc++_static.a
``默认情况下将使用 c++_static``
以下出处：https://developer.android.com/ndk/guides/cpp-support#libc
```
LLVM 的 libc++ 是 C++ 标准库，自 Lollipop 以来 Android 操作系统便一直使用该库，并且从 NDK r18 开始成为 NDK 中唯一可用的 STL。
```

### Gradle生成的cmake命令的路径
command + shift + . 显示隐藏文件
```
当前工程的目录/.externalNativeBuild/cmake/debug/armeabi-v7a/cmake_build_command.txt
```
或者
```
<project-root>/<module-root>/.cxx/cmake/<build-type>/<ABI>/
```
