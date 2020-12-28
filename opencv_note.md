### 编译安卓ndk库

从github下载源码，进入到源码跟目录，创建build文件夹，进入build文件夹，执行下边的编译指令
```
opencv编译指令

export ANDROID_NDK=/Users/liushichao/Library/Android/sdk/ndk/21.0.6113669
export ANDROID_ABI=armeabi-v7a
export ANDROID_NATIVE_API_LEVEL=android-24
export ANDROID_TOOLCHAIN_NAME=arm-linux-androideabi-clang

cmake			       \
  -DANDROID_NDK=${ANDROID_NDK} \
  -DANDROID_ABI=${ANDROID_ABI} \
  -DANDROID_NATIVE_API_LEVEL=${ANDROID_NATIVE_API_LEVEL} \
  -DBUILD_SHARED_LIBS=1 \
  -DCMAKE_TOOLCHAIN_FILE=$ANDROID_NDK/build/cmake/android.toolchain.cmake \
  -DANDROID_TOOLCHAIN_NAME=${ANDROID_TOOLCHAIN_NAME} \
  ..

make -j8

```


### 注意cv::Mat()的宽高参数

前边是高，后边是宽，不要弄反了

```
Mat (int rows, int cols, int type);
```
