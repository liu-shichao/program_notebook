engine\native\cocos\network\Downloader-curl.cpp:670



```
IDownloadTask *DownloaderCURL::createCoTask(std::shared_ptr<const DownloadTask> &task) {
    DownloadTaskCURL *coTask = ccnew DownloadTaskCURL;
    coTask->init(task->storagePath, _impl->hints.tempFileNameSuffix);        // 这里会读写一个静态的set，判断是否两个任务写入同一个文件，如果这个代码在多线程调用可能会不安全，会写入同一个文件

    DLLOG("    DownloaderCURL: createTask: Id(%d)", coTask->serialId);

    _impl->addTask(task, coTask);
    _impl->run();

    if (auto sche = _scheduler.lock()) {
        sche->resumeTarget(this);
    }
    return coTask;
}


```
