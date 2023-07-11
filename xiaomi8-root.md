
```
1.浏览器搜索miui解锁，上小米官网上申请解锁小米手机

2.可能需要三天左右，审核通过后，还是在哪个申请解锁的网站上下载一个解锁工具，需要用windows电脑，这里注意会有坑，在usb3.0的电脑上驱动有问题，解锁工具识别不出来手机连接了，需要下载个辅助软件，里面有修复小米解锁3.0驱动的问题，这个软件名字忘了，当时搜索识别不到小米8手机时候搜到的，有个回复里面提到的，后边到单位看下电脑上的软件名字再补上。

3.下载开发板/测试版线刷包，https://xiaomirom.com/download/mi-8-dipper-weekly-9.9.3/#china-fastboot

4.下载小米的线刷工具，注意下边的三个选项选择保留数据，千万不要选默认的第三个，那个会重新锁上BL， https://xiaomirom.com/download-xiaomi-flash-tool-miflash/

4.5. 线刷包需要解压成文件夹，然后工具里选择哪个文件夹，
4.6. 刷机结束后会提示错误，MiFlash 错误 Not catch checkpoint 解决方法， 这个不用管，是正常的，手机多等会就开机了，https://miuiver.com/miflash-error-not-catch-checkpoint/

5.点安全中心-应用管理-权限-root权限管理，勾选下边的选项，点开始就行了，这样是基本的root了

6.解锁system分区，输入adb root，给adb root权限，然后执行 adb disable-verity ，重启手机，完成
```
