打开xcode就卡死的解决办法

：原因：每次都会加载错误文件日志，恢复上次被强制退出的环境

 ```
 rm -rf ~/Library/Saved\ Application\ State/com.apple.dt.Xcode.savedState
 ```
