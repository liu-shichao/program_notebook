### 7.上传插件到gradle官方仓库

参考链接： https://plugins.gradle.org/docs/submit

1.引入插件 id "com.gradle.plugin-publish" version "0.12.0"

```
plugins {
    // Apply the Java Gradle plugin development plugin to add support for developing Gradle plugins
    id 'java-gradle-plugin'

    // Apply the Groovy plugin to add support for Groovy
    id 'groovy'
    id 'maven-publish'
    id "com.gradle.plugin-publish" version "0.12.0"
}
```

2.填写发布信息

```
//publish to gradle plugin portal
pluginBundle {
    website = 'https://github.com/liu-shichao/ament_gradle_plugin'
    vcsUrl = 'https://github.com/liu-shichao/ament_gradle_plugin'
    description = 'forked from ros2-java/ament_gradle_plugin'
    tags = ['ament', 'rcljava', 'robotics', 'ros2']

    plugins {
        ament {
            id = 'com.github.liu-shichao.gradles'
            displayName = 'A Gradle plugin for building Java and Android-based ROS2 projects'
        }
    }
}
```

3.执行发布task

```
./gradlew publishPlugins
```



### 6.引入android依赖插件

在为android编写gradle插件时候，需要依赖android的插件包，方法如下

```
repositories {
    jcenter()
    google()
}

dependencies {
implementation 'com.android.tools.build:gradle:3.6.4'
}
```



### 5.使用gradle插件
1.引入库

mavenLocal()是在本地查找，仓库位置/Users/liushichao/.m2/repository/
```
buildscript {
  repositories {
    google()
    jcenter()
    mavenCentral()
    mavenLocal()
      maven {
          url("/Users/liushichao/workspace/gradle/ament_gradle_plugin_release/ament_gradle_plugin/repo")
      }
      maven {
          url("https://plugins.gradle.org/m2/")
      }

  }
```

### 4.发布gradle插件


参考链接：https://juejin.cn/post/6887581345384497165

```
1.在build.gradle中添加id 'maven-publish'

plugins {
    // Apply the Java Gradle plugin development plugin to add support for developing Gradle plugins
    id 'java-gradle-plugin'

    // Apply the Groovy plugin to add support for Groovy
    id 'groovy'

    id 'maven-publish'
}

2.加入publishing字段

publishing {
    publications {
        // 这里的 hello 可以任意命名
        hello(MavenPublication) {
            // 插件的组ID，建议设置为插件的包名
            groupId = 'com.lenebf.plugin'
            // 翻译过来是 工件ID，我的理解是插件的名字
            artifactId = 'hello'
            version = '0.0.1'
            // 组件类型，我们的插件其实就是Java组件
            from components.java
        }
    }
}

3.执行./gradlew tasks查看全部的task

4. 执行./gradlew publishHelloPublicationToMavenLocal进行发布，会自动编译
会自动发布到本地仓库/Users/liushichao/.m2/repository 

5. 也可以自定义仓库的位置

publishing {
    ...
    repositories {
        maven {
            // $rootDir 表示你项目的根目录
            url = "$rootDir/repo"
        }
    }
}

然后会多出一个task，执行这个task(一定要看清，不要选错了，这里因为选错了查了好久的原因)
./gradlew publishHelloPublicationToMavenRepository


```


### 3.创建gradle插件

参考链接：https://juejin.cn/post/6887581345384497165

```
1.创建空文件夹
2.执行gradle init
3.按照提示选择即可
```

### 2.finalizedBy在指定task结束后调用另一个task

```
参考连接 https://stackoverflow.com/questions/32878383/gradle-how-to-run-custom-task-after-an-android-library-is-built/47744013
assembleRelease.finalizedBy(copyAARToCommonLibs)
```

### 1.在gradle脚本中添加shell命令


在要执行的build.gradle文件夹中添加如下命令

```
task execTask(type: Exec) {
  workingDir "/Users/liushichao/"
  if (System.getProperty('os.name').toLowerCase(Locale.ROOT).contains('windows')) {
    commandLine 'cmd', '/c', 'mycommand'
  } else {
    commandLine 'sh', '-c', 'touch ./123.zz'
    //commandLine 'sh', './123.sh'
  }
}

```

运行gradle execTask即可执行对应的命令
