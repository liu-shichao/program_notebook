### 修改appId

```
android {
        defaultConfig {
            applicationId "com.example.myapp"
            minSdkVersion 15
            targetSdkVersion 24
            versionCode 1
            versionName "1.0"
        }
        ...
    }
    
```
    
    
### adb命令

1.结束app进程

com.liushichao.myapp是appid，可以用adb shell top命令查看
``
adb shell am force-stop com.liushichao.myapp
``
