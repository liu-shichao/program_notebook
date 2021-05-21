### 2.ide调试动态库

在ide中调试动态库，需要确保以下几项配置都正确：

```
1.在project栏（中间栏）中选择要调试的可执行文件的工程
2.点击运行模式栏（最左边栏）选择Debug模式
3.点击project栏（中间栏）最右边的齿轮按钮，选择Libraries，点击add path，选择要调试的库的路径，点击ok
4.点击菜单栏中的Show View，Modules，打开Modules View窗口
5.点击菜单栏的debug按钮，加载完后，Modules中会显示加载的库文件（确保库文件是debug模式编译的）
6.在modules view中选择要调试的库，右键点击，选择load symbols,等待一段时间后下边的信息栏中显示Symbols:loaded
7.在库文件的源码中打断点即可进行调试

```

### 1.启用系统函数

问题：
在qnx中使用 unistd.h中的access函数判断文件是否存在，会提示找不到access函数。

原因：
在qnx系统的unistd.h头文件中，会有下边的宏定义的判断
#if defined(__EXT_POSIX1_198808)
extern int access(const char *__path, int __mode);

解决方法：
在用到系统函数的头文件中定义下边的宏
#define _QNX_SOURCE 
