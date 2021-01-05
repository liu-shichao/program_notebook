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
