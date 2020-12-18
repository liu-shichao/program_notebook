### 交叉编译安卓ndk版本 (cross compile grpc c++ cpp for android ndk on mac)


先在mac上编译一遍mac版本的，因为后边要用到其中的两个工具，[参考链接](https://github.com/grpc/grpc/blob/e33849682c410452596ebf008a2b984e388e4f99/test/distrib/cpp/run_distrib_test_raspberry_pi.sh#L29)

```
cmake -DCMAKE_TOOLCHAIN_FILE=/Users/liushichao/Library/Android/sdk/ndk/21.0.6113669/build/cmake/android.toolchain.cmake \
 -DANDROID_ABI=armeabi-v7a\
 -DANDROID_PLATFORM=android-26\
 -DANDROID_STL=c++_static\
 -DRUN_HAVE_STD_REGEX=0\
 -DRUN_HAVE_POSIX_REGEX=0\
 -DRUN_HAVE_STEADY_CLOCK=0\
	-DCMAKE_INSTALL_PREFIX=/Users/liushichao/grpc/install \
	../..
```




### 链接错误

example/helloworld

错误提示：

```
Greeter received: RPC failed
```

解决方法：

mac关闭服务的时候不要用``control + z`` ，要用 ``control + c``
```
control + z 
会提示
zsh: suspended  ./greeter_server
```
