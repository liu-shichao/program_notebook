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

### android请求权限

```
1.需要手动添加androidmanifest.xml中
    <uses-permission android:name="android.permission.CAMERA"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    
    WRITE_EXTERNAL_STORAGE包含READ_EXTERNAL_STORAGE权限，所以可以只写WRITE_EXTERNAL_STORAGE
    
2.   
    1.确认build.gradle中的compileSdkVersion是大于28的，如果不报错也没关系
    android {
        ....
        
        compileSdkVersion 28
        
        ....
    }
    2.在顶层中添加依赖
    
        dependencies {
          ...
          
          def activity_version = "1.2.0-alpha08"
          implementation "androidx.activity:activity:$activity_version"
          
          ...
        }

    3.在代码中需要请求权限的地方加入下边的代码
    // Permissions for Android 6+
    if (!ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.CAMERA) ||
            !ActivityCompat.shouldShowRequestPermissionRationale(this,Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
      ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.CAMERA}, 1);
    } else {
      Toast.makeText(this,"已拒绝权限，请在应用管理中手动打开！！！", Toast.LENGTH_SHORT).show();
    }

    if (savedInstanceState != null) {
      isWorking = savedInstanceState.getBoolean(IS_WORKING);
    }
```
