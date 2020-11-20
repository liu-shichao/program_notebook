### 2.asio库提示找不到string_view

解决方法：在build.gradle中将ndk指定为21以后的版本

```

android {
    compileSdkVersion 28
    buildToolsVersion "28.0.2"
    publishNonDefault true
    ndkVersion "21.0.6113669" // e.g.,  ndkVersion '21.3.6528147'
    ...

```


### 提示找不到jni函数的实现

解决方法：将生成aar包的工程清理一下重新编译，将调用app的工程也清理下，替换aar进行重新编译，反复多次，直到成功为止
