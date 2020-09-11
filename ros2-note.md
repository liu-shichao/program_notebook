### Ros2创建msg依赖其他msg

0.创建xxx.msg文件，这里要注意，必须大写字母开头

1.在xxx.msg中添加要依赖的msg，例如：
```
#msg文件中可以用#作为注释
std_msgs/Header header # Header timestamp should be acquisition time of image
                             # Header frame_id should be optical frame of camera
sensor_msgs/CameraInfo camera_info
int64 frame_addr
```

2.在CMakeList.txt文件中，加入下边的代码，主要是DEPENDENCIES那一项，如果不指定会编译不通过

```
find_package(std_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)


rosidl_generate_interfaces(${PROJECT_NAME}
  "msg/DetectedObject.msg"
  "msg/DetectedObjects.msg"
  "msg/InstantiatedObject.msg"
  "msg/InstantiationLabel.msg"
  "msg/UpdateFrame.msg"
  "msg/Gps.msg"
  DEPENDENCIES std_msgs sensor_msgs    ##这行很重要
)
```

3.在package.xml中添加下边的内容

```
  <build_depend>rosidl_default_generators</build_depend>
  <exec_depend>rosidl_default_runtime</exec_depend>
  <build_depend>std_msgs</build_depend>
  <exec_depend>std_msgs</exec_depend>
  <build_depend>sensor_msgs</build_depend>
  <exec_depend>sensor_msgs</exec_depend>
```

### ros2-java的版本

ros2-java中用的ros2应该是crystal版本的，最新的是foxy，ros2版本列表如下

```
http://docs.ros2.org/eloquent
http://docs.ros2.org/dashing
http://docs.ros2.org/crystal
http://docs.ros2.org/bouncy
http://docs.ros2.org/ardent
http://docs.ros2.org/beta3
http://docs.ros2.org/beta2
http://docs.ros2.org/beta1
http://docs.ros2.org/alpha8

```
android版的ros2可以调试运行了

```
build.gradle文件中，加入

android{

  //...

  ndk{
    abiFilters "armeabi-v7a"
  }
  
  //...

}

在运行按钮左边选择ros2_talker_android，点debug按钮就可以了

```
