### 3.推送某个文件夹到安卓设备
将电脑上的当前目录的data 文件夹推送到安卓设备的/data/vision_module/目录下，结束后/data/vision_module/目录下会有一个data文件夹
```
adb push ./data/ /data/vision_module/
```

### 2.删除链接的某个设备
首先执行adb devices查看链接的设备，然后执行下边的命令删除其中的某一项
```
adb -s 192.168.1.3:5555 kill-server
```


### 1.查看adb链接的设备列表

```
adb devices
```

运行结果如下

```
List of devices attached
1678d92a	device
192.168.1.3:5555	device
```
