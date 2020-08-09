# 记录常用cmake命令

### 1.if语句
执行``cmake -DUSER_DEFINE=liushichao ./``，返回err.
```
if(NOT "${USER_DEFINE}" STREQUAL "liushichao")
  MESSAGE("ok.")
else()
  MESSAGE("err.")
endif()
```

### 2.get_filename_component

获取第二个参数的绝对路径，存到第一个参数重，执行完后 ``ANDROID_NDK_EXPECTED_PATH`` 中存储的事当前路径的绝对路径
```
get_filename_component(ANDROID_NDK_EXPECTED_PATH
    "./" ABSOLUTE)
```

### 3.使用环境变量

``$ENV{xxx}``可以获取环境变量xxx
```
MESSAGE("$ENV{PATH}")
```

### 4.cmake路径

为了统一路径中的分割符windows ``c:\xx`` linux ``/usr/xxx``，cmake定义了统一的分割符``/``的路径表示方式，可以用file命令进行转换
```
file(TO_CMAKE_PATH "<path>" <variable>)
file(TO_NATIVE_PATH "<path>" <variable>)
```
### 5.指定c++标准库版本
```
cmake_minimum_required(VERSION 3.10)

# set the project name and version
project(Tutorial VERSION 1.0)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
```
### 6.include命令
通过定义xxx.cmake，可以重用cmake的代码
```
include(xxx.cmake)
```

### 7.find_path
在``/Users/liushichao/workspace``下创建``1.txt``,执行下边代码，返回``/Users/liushichao/workspace``。
如果没有找到，返回``TXT_PATH-NOTFOUND``
这个TXT_PATH如果被设置后，以后不会被更新
```
find_path(TXT_PATH "1.txt" /Users/liushichao/workspace/123 /Users/liushichao/workspace)
MESSAGE("${TXT_PATH}")
```
