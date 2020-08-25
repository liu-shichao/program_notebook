# java版本 1.8

java version "1.8.0_261"

# Gradle版本 3.5.0


# NDK版本 r21

```
export ANDROID_NDK=/Users/liushichao/Library/Android/sdk/ndk/16.1.4479499
export ANDROID_NDK=/Users/liushichao/Library/Android/sdk/ndk/21.0.6113669
```


# define paths
```
ROOT_DIR=${HOME}/workspace/ros2/ros2_android
AMENT_WORKSPACE=${ROOT_DIR}/ament_ws
ROS2_ANDROID_WORKSPACE=${ROOT_DIR}/ros2_android_ws
```

# define paths
```
ROOT_DIR=${HOME}/workspace/ros2
AMENT_WORKSPACE=${ROOT_DIR}/ament_ws
ROS2_ANDROID_WORKSPACE=${ROOT_DIR}/ros2_android_ws
```

# pull and build ament
```
mkdir -p ${AMENT_WORKSPACE}/src
cd ${AMENT_WORKSPACE}
wget https://raw.githubusercontent.com/esteve/ament_java/master/ament_java.repos
vcs import ${AMENT_WORKSPACE}/src < ament_java.repos
colcon build
```

# android build configuration
```
export PYTHON3_EXEC="$( which python3 )"
export ANDROID_ABI=armeabi-v7a
export ANDROID_NATIVE_API_LEVEL=android-21
export ANDROID_TOOLCHAIN_NAME=arm-linux-androideabi-clang
```

# pull and build ros2 for android
```
mkdir -p ${ROS2_ANDROID_WORKSPACE}/src
cd ${ROS2_ANDROID_WORKSPACE}
wget https://raw.githubusercontent.com/esteve/ros2_java/master/ros2_java_android.repos

     https://raw.githubusercontent.com/esteve/ros2_java/$ROS2_JAVA_BRANCH/ros2_java_android.repos
     https://raw.githubusercontent.com/esteve/ros2_java/master/ros2_java_android.repos
     https://raw.githubusercontent.com/esteve/ament_java/master/ament_java.repos

vcs import ${ROS2_ANDROID_WORKSPACE}/src < ros2_java_android.repos
source ${AMENT_WORKSPACE}/install/local_setup.sh
ament build --isolated --skip-packages test_msgs \
  --cmake-args \
  -DPYTHON_EXECUTABLE=${PYTHON3_EXEC} \
  -DCMAKE_TOOLCHAIN_FILE=$ANDROID_NDK/build/cmake/android.toolchain.cmake \
  -DANDROID_FUNCTION_LEVEL_LINKING=OFF \
  -DANDROID_NATIVE_API_LEVEL=${ANDROID_NATIVE_API_LEVEL} \
  -DANDROID_TOOLCHAIN_NAME=${ANDROID_TOOLCHAIN_NAME} \
  -DANDROID_STL=gnustl_shared \
  -DANDROID_ABI=${ANDROID_ABI} \
  -DANDROID_NDK=${ANDROID_NDK} \
  -DTHIRDPARTY=ON \
  -DCOMPILE_EXAMPLES=OFF \
  -DCMAKE_FIND_ROOT_PATH="$AMENT_WORKSPACE/install;$ROS2_ANDROID_WORKSPACE/install_isolated" \
  -- \
  --parallel \
  --ament-gradle-args \
  -Pament.android_stl=gnustl_shared -Pament.android_abi=$ANDROID_ABI -Pament.android_ndk=$ANDROID_NDK --



distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.4-all.zip
换成
distributionUrl=https\://services.gradle.org/distributions/gradle-4.6-all.zip



See also "/Users/liushichao/workspace/ros2/ros2_android_ws/build_isolated/rcljava_common/CMakeFiles/CMakeOutput.log".



action_msgs
rosidl_typesupport_cpp
rcl_lifecycle
rcljava_common
ros2/rcl_interfaces
ament_cmake_export_jars
rclandroid
ros2_talker_android
ros2_listener_android

ament build --isolated --only-packages ros2_listener_android \
  --cmake-args \
  -DPYTHON_EXECUTABLE=${PYTHON3_EXEC} \
  -DCMAKE_TOOLCHAIN_FILE=$ANDROID_NDK/build/cmake/android.toolchain.cmake \
  -DANDROID_FUNCTION_LEVEL_LINKING=OFF \
  -DANDROID_NATIVE_API_LEVEL=${ANDROID_NATIVE_API_LEVEL} \
  -DANDROID_TOOLCHAIN_NAME=${ANDROID_TOOLCHAIN_NAME} \
  -DANDROID_STL=gnustl_shared \
  -DANDROID_ABI=${ANDROID_ABI} \
  -DANDROID_NDK=${ANDROID_NDK} \
  -DTHIRDPARTY=ON \
  -DCOMPILE_EXAMPLES=OFF \
  -DCMAKE_FIND_ROOT_PATH="$AMENT_WORKSPACE/install;$ROS2_ANDROID_WORKSPACE/install_isolated" \
  -- \
  --parallel \
  --ament-gradle-args \
  -Pament.android_stl=gnustl_shared -Pament.android_abi=$ANDROID_ABI -Pament.android_ndk=$ANDROID_NDK --






/Users/liushichao/workspace/ros2/ros2_android_ws/install_isolated/lifecycle_msgs/include/lifecycle_msgs/msg/transition__struct.h

lifecycle_msgs__msg__Transition__TRANSITION_SHUTDOWN
lifecycle_msgs__msg__Transition__TRANSITION_DESTROY



ros2/rosidl:
  type: git
  url: https://github.com/ros2/rosidl.git
  version: 0.5.1


ros2/rcl:
  type: git
  url: https://github.com/ros2/rcl.git
  version: 0.5.1


改成bouncy版本
ros2/rcl_interfaces:
  type: git
  url: https://github.com/ros2/rcl_interfaces.git
  version: bouncy


rcljava_common错误

/Users/liushichao/workspace/ros2/ros2_android/ament_ws/install/ament_java_resources/share/ament_index/resource_index/templates
拷贝一份到下方路径
/Users/liushichao/workspace/ros2/ros2_android/ament_ws/install/ament_flake8/share/ament_index/resource_index/templates


java 8 
1.安装完要删除之前的版本
2.设置JAVA_HOME为java8的jdk的文件路径

gradle 3.5
brew install /Users/liushichao/Desktop/ros2编译/安装包/gradle.rb

local.properties里修改
ndk.dir=/Users/liushichao/Library/Android/sdk/ndk/16.1.4479499
sdk.dir=/Users/liushichao/Library/Android/sdk

export ANDROID_NDK=/Users/liushichao/Library/Android/sdk/ndk/16.1.4479499

修改gradlew的权限，sudo chmod +x /Users/liushichao/workspace/ros2/ros2_android/ros2_android_ws/src/ros2_java/ros2_android_examples/ros2_listener_android/gradlew

修改gradlew 
/Users/liushichao/workspace/ros2/ros2_android/ros2_android_ws/src/ros2_java/ros2_android_examples/ros2_talker_android/gradle/wrapper/gradle-wrapper.properties

distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.4-all.zip
换成
distributionUrl=https\://services.gradle.org/distributions/gradle-4.6-all.zip


试一下编译ament的时候是用--symblelink那个选项
```
### 问题1:
描述：更新NDK到r18版本进行编译，替换原来的`` -DANDROID_STL=gnustl_shared``为`` -DANDROID_STL=c++_shared``,导致``fastrtps``包编译报错，错误信息为

```
unknown type name 'string_view'; did you mean 'std::string_view'?
```

原因：``libc++ exposes std::basic_string_view for any -std= but libstdc++ only for C++17.``

解决方案：在``ros2_android_ws/src/eProsima/Fast-RTPS/thirdparty/asio/asio/include/asio/detail/config.hpp``中搜索``define ASIO_HAS_STD_EXPERIMENTAL_STRING_VIEW 1``，将搜到的几行全部注释掉










ddsi_conn_write failed -1 then you’ll need to increase your system wide UDP packet size:

$ sudo sysctl -w net.inet.udp.recvspace=209715
$ sudo sysctl -w net.inet.udp.maxdgram=65500

### 问题2:
描述： /Volumes/Android/buildbot/src/android/ndk-release-r17/external/libcxx/../../external/libcxxabi/src/abort_message.cpp:73:

解决方案，这是ndk的bug，需要升级到r18beta版以上

### 问题3:
模拟器运行失败

解决方案，root手机，在手机上执行dbg生成头文件

小米8 root命令

```
adb root

adb disable-verity

adb reboot
```


### 将自己创建的包加入到android的apk文件中

只需要在android工程的package.xml中加入下边的依赖语句

```
  <build_depend>my_package</build_depend>
  <exec_depend>my_package</exec_depend>
```
