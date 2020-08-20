## android NDK 利用jni从c++中读写外部存储的文件sdcard

### 获取访问外部存储的权限

1.在androidMainfest.xml中添加访问外部存储的读写权限

```
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

完整版如下

```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
      package="org.ros2.examples.android.talker"
      android:versionCode="1"
      android:versionName="1.0">
    <uses-permission android:name="android.permission.CAMERA"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-feature android:name="android.hardware.camera"/>
    <uses-feature android:name="android.hardware.camera.autofocus"/>
    <uses-feature android:name="android.hardware.camera.front"/>
    <uses-feature android:name="android.hardware.camera.front.autofocus"/>
    <application android:label="@string/app_name" android:icon="@drawable/ic_launcher">
        <activity android:name="ROS2TalkerActivity"
                  android:label="@string/app_name">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-sdk android:minSdkVersion="8" />
</manifest>

```


2.修改build.gradle,引入andoridx库，为第三步做准备

```
在顶层添加依，如果是新版本的gradle插件，可以把下边的compile换成implementation。

dependencies {
  def appcompat_version = "1.1.0"
  compile "androidx.appcompat:appcompat:$appcompat_version"
  // For loading and tinting drawables on older versions of the platform
  compile "androidx.appcompat:appcompat-resources:$appcompat_version"
}

```

完整版本如下

```
apply plugin: 'com.android.application'
apply plugin: 'org.ros2.tools.gradle'
apply plugin: 'me.tatarka.retrolambda'

sourceCompatibility = JavaVersion.VERSION_1_8
targetCompatibility = JavaVersion.VERSION_1_8

android {
  compileSdkVersion 28
  buildToolsVersion "25.0.2"
  defaultConfig {
    minSdkVersion 24
    targetSdkVersion 26
//    ndk {
//      abiFilters "armeabi-v7a"
//    }
    externalNativeBuild {
      cmake {
        cppFlags "-frtti -fexceptions"
        abiFilters 'armeabi-v7a'
      }
    }
  }
  externalNativeBuild {
    cmake {
      path "CMakeLists.txt"
    }
  }
  sourceSets {
    main {
      jniLibs.srcDirs = ['src/main/jniLibs']
    }
  }

//  dependencies {
//    def appcompat_version = "1.1.0"
//
//    implementation "androidx.appcompat:appcompat:$appcompat_version"
//    // For loading and tinting drawables on older versions of the platform
//    implementation "androidx.appcompat:appcompat-resources:$appcompat_version"
//  }
}

buildscript {
  repositories {
    jcenter()
    mavenCentral()
    mavenLocal()
    maven {
      url "https://plugins.gradle.org/m2/"
    }
  }

  dependencies {
    classpath 'com.android.tools.build:gradle:2.3.3'
    classpath 'gradle.plugin.org.ros2.tools.gradle:ament:0.7.0'
    classpath 'me.tatarka:gradle-retrolambda:3.6.1'
  }
}

repositories {
   mavenCentral()
  google()
}

dependencies {
  def appcompat_version = "1.1.0"
  compile "androidx.appcompat:appcompat:$appcompat_version"
  // For loading and tinting drawables on older versions of the platform
  compile "androidx.appcompat:appcompat-resources:$appcompat_version"
}

```

3.在程序的入口函数中添加如下代码，我添加在了onCreate中，引入相关的头文件，要执行完第二步才有这些头文件

```

import androidx.core.app.ActivityCompat;

```

```

 if (!ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.CAMERA) ||
            !ActivityCompat.shouldShowRequestPermissionRationale(this,Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
      ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.CAMERA}, 1);
    } else {
      Toast.makeText(this,"已拒绝权限，请在应用管理中手动打开！！！", Toast.LENGTH_SHORT).show();
    }
```

完整代码如下

```
/* Copyright 2016-2017 Esteve Fernandez <esteve@apache.org>
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package org.ros2.examples.android.talker;

import android.Manifest;
import android.app.Activity;
import android.os.Bundle;
import android.os.Environment;
import android.util.Log;
import android.view.View;
import android.view.View.OnClickListener;
import android.widget.Button;
import android.widget.Toast;
import androidx.core.app.ActivityCompat;

import org.ros2.rcljava.RCLJava;

import org.ros2.android.activity.ROSActivity;

import java.io.File;

public class ROS2TalkerActivity extends Activity {

  private static final String IS_WORKING = "isWorking";

  private TalkerNode talkerNode;

  private static String logtag = ROS2TalkerActivity.class.getName();

  private boolean isWorking;





  /** Called when the activity is first created. */
  @Override
  public final void onCreate(final Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);

    if (!ActivityCompat.shouldShowRequestPermissionRationale(this, Manifest.permission.CAMERA) ||
            !ActivityCompat.shouldShowRequestPermissionRationale(this,Manifest.permission.WRITE_EXTERNAL_STORAGE)) {
      ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.CAMERA}, 1);
    } else {
      Toast.makeText(this,"已拒绝权限，请在应用管理中手动打开！！！", Toast.LENGTH_SHORT).show();
    }

    if (savedInstanceState != null) {
      isWorking = savedInstanceState.getBoolean(IS_WORKING);
    }

    Button buttonStart = (Button)findViewById(R.id.buttonStart);
    buttonStart.setOnClickListener(startListener);

    Button buttonStop = (Button)findViewById(R.id.buttonStop);
    buttonStop.setOnClickListener(stopListener);


    String SDCardRoot =  Environment.getExternalStorageDirectory().getAbsolutePath() + File.separator;
    Log.e(logtag, SDCardRoot);

//    RCLJava.rclJavaInit();

//    talkerNode = new TalkerNode("android_talker_node", "chatter");

    changeState(isWorking);
  }

  // Create an anonymous implementation of OnClickListener
  private OnClickListener startListener = new OnClickListener() {
    public void onClick(final View view) {
      Log.d(logtag, "onClick() called - start button");
      Toast
          .makeText(ROS2TalkerActivity.this, "The Start button was clicked.",
                    Toast.LENGTH_LONG)
          .show();
      Log.d(logtag, "onClick() ended - start button");
      Button buttonStart = (Button)findViewById(R.id.buttonStart);
      Button buttonStop = (Button)findViewById(R.id.buttonStop);
      changeState(true);
      new Thread(new Runnable() {
        @Override
        public void run() {
          int c = TestJni.add(1, 2);
          Log.e(logtag, "tstjni add = " + c);
        }
      }).start();
      //TestJni.createFile();
    }
  };

  // Create an anonymous implementation of OnClickListener
  private OnClickListener stopListener = new OnClickListener() {
    public void onClick(final View view) {
      Log.d(logtag, "onClick() called - stop button");
      Toast
          .makeText(ROS2TalkerActivity.this, "The Stop button was clicked.",
                    Toast.LENGTH_LONG)
          .show();
      changeState(false);
      Log.d(logtag, "onClick() ended - stop button");
      talkerNode.stop();
    }
  };

  private void changeState(boolean isWorking) {
    this.isWorking = isWorking;
    Button buttonStart = (Button)findViewById(R.id.buttonStart);
    Button buttonStop = (Button)findViewById(R.id.buttonStop);
    buttonStart.setEnabled(!isWorking);
    buttonStop.setEnabled(isWorking);
    if (isWorking){
//      getExecutor().addNode(talkerNode);
//      talkerNode.start();
    } else {
//      talkerNode.stop();
//      getExecutor().removeNode(talkerNode);
    }
  }

  @Override
  protected void onSaveInstanceState(Bundle outState) {
    if (outState != null) {
      outState.putBoolean(IS_WORKING, isWorking);
    }
    super.onSaveInstanceState(outState);
  }
}


```

上边配置好了，就能在jni中用c/c++常用的方法进行文件读写了，也可用opencv的imread读取图片了


jni写文件示例,

JAVA代码

```
   public static native int nativeCreateFile(String filePath);
    public static void createFile()
    {
        //File sdcard = Environment.getExternalStorageDirectory();
        //String fileDir = sdcard.getAbsolutePath() + "/testfolder/test.txt";
        nativeCreateFile("/sdcard/test.txt");
    }
```

C++代码

```

  JNIEXPORT jint JNICALL
Java_org_ros2_examples_android_talker_TestJni_nativeCreateFile(JNIEnv *env, jclass clazz,
                                                               jstring file_path) {
    // TODO: implement nativeCreateFile()
    const char* str = env->GetStringUTFChars(file_path, 0);
    LOGE("file from jni : %s", str);
    FILE* file = fopen(str,"w+");
    if (file != NULL) {
        fputs("jni write sdcard external storage test.", file);
        fflush(file);
        fclose(file);
    }
    else
    {
        LOGE("again, open failed ... errno is : %d, means : %s", errno, strerror(errno));
    }
    env->ReleaseStringUTFChars(file_path, str);
    return 0;
}


```
