# 记录常用cmake命令


### 9. target_compile_definitions

作用：#define xxxxx zzzz

用法：

```
target_compile_definitions(hello MY_DEFINE="nihao")
```

如果在编译的main.cpp中，写入如下代码的话

```
int main()
{
#ifdef MY_DEFINE
  cout<< MY_DEFINE << endl;
#else
  cout << "undefine" << endl;
#endif
  return 0;
}
```

会输出 ``nihao``


### 8 指定编译release版本或debug版本

注意：如果不使用CMAKE_BUILD_TYPE参数，则默认是Debug

```
-DCMAKE_BUILD_TYPE=Debug

-DCMAKE_BUILD_TYPE=Release
```

例子：

```
mkdir Release  
cd Release  
cmake -DCMAKE_BUILD_TYPE=Release ..  
make 
```

```
mkdir Debug  
cd Debug  
cmake -DCMAKE_BUILD_TYPE=Debug ..  
make  
```


### 7 MESSAGE

有些情况下需要指定消息的错误等级才能显示出来这个消息，用来调试用，例如
```
  message(FATAL_ERROR
        "The RMW implementation has been specified as "
        "'${requested_rmw_implementation}' "
        "through the environment variable 'RMW_IMPLEMENTATION', "
        "however this needs to match the RMW implementation "
        "'${default_rmw_implementation}', "
        "which was specified when the 'rmw_implementation' package was built.")
```


### 6. add_dependencies()


### 5. add_custom_command()


### 4. add_custom_target

这个命令不会创建目标文件

### 3. ${PROJECT_SOURCE_DIR} 

TODO 测试后补充说明


### 2. file命令（神器）

下边命令能将opencv的全部库文件都添加到link中

```
file(GLOB_RECURSE dyso "/Users/liushichao/Exercise/build_opencv_4.3.0/lib/*.dylib")
target_link_libraries(test_sort
${dyso}
)
MESSAGE("${dyso}")
```

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
可以指定包含的文件的全路径，或者让cmake去搜索，搜索顺序：1.CMAKE_MODULE_PATH变量指定的路径 2.cmake自己的Modules文件夹``/usr/local/Cellar/cmake/3.18.1/share/cmake/Modules``
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

### 8.configure_file
将输入文件，转换成输出文件，可以自定义变量，改变输出文件中的值
例如在cmakelist文件夹下定义一个foo.h.in文件，或者在其他目录里创建，然后cmakelist.txt文件中指明相对路径
在foo.h.in中可以加入如下定义
```
//foo.h.in

#cmakedefine XXXX "@XXXX@"
@bbb@

```

编辑CMakeLists.txt

```
//CMakeLists.txt

set(bbb "nihao")
set(XXXX "hahah")
configure_file(foo.h.in foo.h @ONLY)
```

会在执行cmake命令的目录里生成foo.h文件，内容如下

```
//foo.h

#define XXXX "hahah"
nihao
```

如果CMakeLists.txt文件中没有写set(bbb "nihao") 也没写 set(XXXX "hahah")，则生成的文件如下

```
//foo.h

/* #undef XXXX */

```

### 9.cmake的function

定义如下，第一个参数是函数名，第二个参数是传入的参数
```
function(func_name list)
  MESSAGE("${list}") #abc
  MESSAGE("${${list}}") #a;b;c
endfunction()
```

调用方法如下

```
set(abc a b c)
func_name(abc)
```

输出

```
abc
a;b;c
```
