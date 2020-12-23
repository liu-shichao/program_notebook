### 4.grpc编译报错的解决方法 thread链接错误

起因：今天将build_isolated中的my_package文件删了，然后重新编译的时候提示报错了

操作命令：

```
# define paths
export ANDROID_NDK=/Users/liushichao/Library/Android/sdk/ndk/21.0.6113669
ROOT_DIR=${HOME}/workspace/sgmm_ros2
AMENT_WORKSPACE=${ROOT_DIR}/ament_ws
ROS2_ANDROID_WORKSPACE=${ROOT_DIR}/ros2_android_ws
# android build configuration
export PYTHON3_EXEC="$( which python3 )"
export ANDROID_ABI=armeabi-v7a
export ANDROID_NATIVE_API_LEVEL=android-24
export ANDROID_TOOLCHAIN_NAME=arm-linux-androideabi-clang
cd ${ROS2_ANDROID_WORKSPACE}
source ${AMENT_WORKSPACE}/install/local_setup.sh


ament build --isolated --only-packages my_package\
  --cmake-args \
  -DBUILD_TESTING=OFF \
  -DPYTHON_EXECUTABLE=${PYTHON3_EXEC} \
  -DCMAKE_TOOLCHAIN_FILE=$ANDROID_NDK/build/cmake/android.toolchain.cmake \
  -DANDROID_FUNCTION_LEVEL_LINKING=OFF \
  -DANDROID_NATIVE_API_LEVEL=${ANDROID_NATIVE_API_LEVEL} \
  -DANDROID_TOOLCHAIN_NAME=${ANDROID_TOOLCHAIN_NAME} \
  -DANDROID_STL=c++_shared \
  -DCMAKE_CXX_STANDARD=17 \
  -DANDROID_ABI=${ANDROID_ABI} \
  -DANDROID_NDK=${ANDROID_NDK} \
  -DProtobuf_DIR=/Users/liushichao/grpc/install/lib/cmake/protobuf \
  -DgRPC_DIR=/Users/liushichao/grpc/install/lib/cmake/grpc \
  -DTHIRDPARTY=ON \
  -DCOMPILE_EXAMPLES=OFF \
  -DCMAKE_FIND_ROOT_PATH="$AMENT_WORKSPACE/install;$ROS2_ANDROID_WORKSPACE/install_isolated" \
  -- \
  --parallel \
  --ament-gradle-args \
  -Pament.android_stl=c++_shared -Pament.android_abi=$ANDROID_ABI -Pament.android_ndk=$ANDROID_NDK --

```

错误提示：第一次编译，提示如下三个错误

```
CMake Error at CMakeLists.txt:58 (add_library):
  Target "my_package" links to target "Threads::Threads" but the target was
  not found.  Perhaps a find_package() call is missing for an IMPORTED
  target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:58 (add_library):
  Target "my_package" links to target "Threads::Threads" but the target was
  not found.  Perhaps a find_package() call is missing for an IMPORTED
  target, or an ALIAS target is missing?


CMake Error at CMakeLists.txt:58 (add_library):
  Target "my_package" links to target "Threads::Threads" but the target was
  not found.  Perhaps a find_package() call is missing for an IMPORTED
  target, or an ALIAS target is missing?
```

如果不管这个，强行再次编译会报如下错误：

```
1.编译能到100%
2.链接出错，报
[100%] Linking CXX shared library libmy_package.so
/Users/liushichao/Library/Android/sdk/ndk/21.0.6113669/toolchains/llvm/prebuilt/darwin-x86_64/lib/gcc/arm-linux-androideabi/4.9.x/../../../../arm-linux-androideabi/bin/ld: error: cannot find -lThreads::Threads
clang++: error: linker command failed with exit code 1 (use -v to see invocation)
```

解决方法：

```
1.尝试注释掉引入的三个grpc相关的库，然后重新编译，编译完成后会报错，然后在加上这三个链接的变量，再次编译就成功了
target_link_libraries(
  ${PROJECT_NAME} 
  ${log-lib}
  lib_opencv
  tensorflowLite
#  ${_REFLECTION}			   <-----------
 # ${_GRPC_GRPCPP}			    <-----------
 # ${_PROTOBUF_LIBPROTOBUF}    <----------
  tensorflowLiteGpuDelegate
  android
  sgmnv_tool)
```

错误原因：

待查。



### 3.交叉编译安卓ndk版本的grpc的demo程序



### 2.交叉编译安卓ndk版本的grpc静态库 (cross compile grpc c++ cpp for android ndk on mac)


先在mac上编译一遍mac版本的，因为后边要用到其中的两个工具，[参考链接](https://github.com/grpc/grpc/blob/e33849682c410452596ebf008a2b984e388e4f99/test/distrib/cpp/run_distrib_test_raspberry_pi.sh#L29)

```
mkdir -p "cmake/build"
pushd "cmake/build"
cmake \
  -DCMAKE_BUILD_TYPE=Release \
  -DgRPC_INSTALL=ON \
  -DgRPC_BUILD_TESTS=OFF \
  -DgRPC_SSL_PROVIDER=package \
  ../..
make -j4 install
popd
```


然后再用ndk的cmake工具链交叉编译安卓的ndk版本
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




### 1.链接错误

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
