# 记录常用cmake命令
执行``cmake -DUSER_DEFINE=liushichao ./``，返回ok.
```
if("${USER_DEFINE}" STREQUAL "liushichao")
  MESSAGE("ok.")
else()
  MESSAGE("err.")
endif()
```
