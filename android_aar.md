## android aar库

### 介绍

AAR（Android ARchive）,是安卓的库，几乎能够包含apk中的全部内容，包括资源和代码

### 生成AAR

可以新建一个AAR模块，或者修改原来生成apk的应用模块，使他打包生成AAR库。

#### 一、将生成apk的应用模块，修改成生成AAR的库模块

1.修改build.gradle文件（对应的要修改的app的模块下的build.gradle）

```
1.删除 applicationId ，如果没有就不用管了

2.修改 apply plugin: 'com.android.application' 为 apply plugin: 'com.android.library'

```

2.修改AndroidManifest.xml

```
主要是去掉这几行，如果有报错的话可以恢复，看看是哪一项报错了，对应解决一下

        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        
        
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
```

3.保存，点击File -> Sync Project With Gradle Files.

4.build -> build apk,如果不成功，需要clean一下再build apk.

### 引用AAR库

引用AAR库分为两种方式，一种是引用编译好的AAR包，另一种是引用源码，现在介绍第一种

1.菜单栏点击 File -> New -> New Module.

2.选择 import .JAR/.AAR Package.

3.选择AAR包的位置，点击FINISH.

4.settings.gradle中添加 include ':app', ':you_module'，之前应该有了include ':app'，在那个基础上修改就行

5.在app模块的build.gradle文件中添加依赖，在顶层位置添加

```
implementation project(":you_module")
```

ok.

注意，如果AAR包里使用的是armeabi-v7a, 而app中默认是arm64-v8a架构的话，AAR包中的so动态连接库不会被打包进apk，需要调整app的架构和aar包中的一致


