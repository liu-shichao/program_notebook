### 启用系统函数

问题：
在qnx中使用 unistd.h中的access函数判断文件是否存在，会提示找不到access函数。

原因：
在qnx系统的unistd.h头文件中，会有下边的宏定义的判断
#if defined(__EXT_POSIX1_198808)
extern int access(const char *__path, int __mode);

解决方法：
在用到系统函数的头文件中定义下边的宏
#define _QNX_SOURCE 
