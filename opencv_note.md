### 3.本地cmake加入opencv库

```
find_package(OpenCV REQUIRED)  #注意大小写
target_include_directories(
  ${PROJECT_NAME}
  PUBLIC
  ${OpenCV_INCLUDE_DIRS}
)

target_link_libraries(
  ${PROJECT_NAME}
  ${OpenCV_LIBS}
)

```


### 2.编译安卓ndk库

从github下载源码，进入到源码跟目录，创建build文件夹，进入build文件夹，执行下边的编译指令

```
export ANDROID_NDK=/Users/liushichao/Library/Android/sdk/ndk/21.0.6113669
export ANDROID_ABI=armeabi-v7a
export ANDROID_NATIVE_API_LEVEL=android-24
export ANDROID_TOOLCHAIN_NAME=arm-linux-androideabi-clang

cmake			       \
  -DANDROID_NDK=${ANDROID_NDK} \
  -DANDROID_ABI=${ANDROID_ABI} \
  -DANDROID_STL=c++_shared  \
  -DANDROID_NATIVE_API_LEVEL=${ANDROID_NATIVE_API_LEVEL} \
  -DBUILD_SHARED_LIBS=1 \
  -DCMAKE_TOOLCHAIN_FILE=$ANDROID_NDK/build/cmake/android.toolchain.cmake \
  -DANDROID_TOOLCHAIN_NAME=${ANDROID_TOOLCHAIN_NAME} \
  -D BUILD_opencv_java=ON \
  -D BUILD_ANDROID_PROJECTS=ON \
        -D WITH_CUDA=OFF \
        -D WITH_MATLAB=OFF \
        -D BUILD_ANDROID_EXAMPLES=OFF \
        -D BUILD_DOCS=OFF \
        -D BUILD_PERF_TESTS=OFF \
        -D BUILD_TESTS=OFF \
        -DCMAKE_INSTALL_PREFIX="/Users/liushichao/source/opencv/install" \
  ..

make -j8


```


### 1.注意cv::Mat()的宽高参数

前边是高，后边是宽，不要弄反了

```
Mat (int rows, int cols, int type);
```
