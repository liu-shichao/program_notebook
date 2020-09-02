## 在gradle脚本中添加shell命令


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
