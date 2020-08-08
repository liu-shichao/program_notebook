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
