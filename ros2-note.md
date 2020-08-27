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

  ...

  ndk{
    abiFilters "armeabi-v7a"
  }
  ...

}

```
