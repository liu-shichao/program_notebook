# 记录常用cmake命令

### 1.if语句
执行``cmake -DUSER_DEFINE=liushichao ./``，返回ok.
```
if("${USER_DEFINE}" STREQUAL "liushichao")
  MESSAGE("ok.")
else()
  MESSAGE("err.")
endif()
```

### 2.

获取第二个参数的绝对路径，存到第一个参数重，执行完后 ``ANDROID_NDK_EXPECTED_PATH`` 中存储的事当前路径的绝对路径
```
get_filename_component(ANDROID_NDK_EXPECTED_PATH
    "./" ABSOLUTE)
```

