### 1. 一个app中多个库的冲突

多个库添加到一个app工程中，会出现很诡异的bug，现象是，我这个模块的功能正常加载运行，但是另一个库在执行某个方法时突然崩掉了，错误日志很简单，只有一行

```
2020-09-09 13:50:18.119 28623-28800/com.sogou.sgmar.demo A/libc: Fatal signal 11 (SIGSEGV), code 1 (SEGV_MAPERR), fault addr 0xfffffff4 in tid 28800 (VlcObject), pid 28623 (ogou.sgmar.demo)
```

#### 方法一：经过彬哥指点，解决方法如下

1.找到加载so的java文件

2.在加载so的代码前添加如下一行代码

```
System.loadLibrary("c++_shared");
```
3.修改后代码如下

```
public class xxxx {
    final static String TAG = "xxxx";

    static {
        try {
            System.loadLibrary("c++_shared");  //add this line
            System.loadLibrary("xxxx_jni");
        } catch (UnsatisfiedLinkError e) {
            Log.e(TAG, e.toString());
        }
    }
}

```

#### 方法二：在build.gradle文件中添加下边的代码

```
android {
        ...
    defaultConfig {
            ...
        externalNativeBuild {
                ...
            cmake {
                cppFlags ""
                arguments "-DANDROID_STL=c++_shared" //add this line
            }
        }
    }
```
