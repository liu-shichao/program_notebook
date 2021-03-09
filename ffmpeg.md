### NDK编译

```
#!/bin/bash
   
export NDK=/Users/liushichao/Library/Android/sdk/ndk/21.0.6113669
export PREBUILD=$NDK/toolchains/llvm/prebuilt
export CROSS_PREFIX=${PREBUILD}/darwin-x86_64/bin/arm-linux-androideabi-
export CC=$PREBUILD/darwin-x86_64/bin/armv7a-linux-androideabi28-clang
export NM=$CROSS_PREFIXnm
export AR=$CROSS_PREFIXar

export PREFIX=./android/armeabi-v7a

function build_so
    {
     ./configure \
        --prefix=$PREFIX \
        --cc=$CC \
        --nm=$NM \
        --ar=$AR \
        --enable-small \
        --disable-programs \
        --disable-avdevice \
        --disable-encoders \
        --disable-muxers \
        --disable-filters \
        --cross-prefix=$CROSS_PREFIX \
        --target-os=android \
        --arch=arm \
        --enable-shared \
        --disable-static \
        --enable-cross-compile
    }

make clean
build_so
make -j4
make install
```

