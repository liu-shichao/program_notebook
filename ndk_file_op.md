### 2.判断目录是否存在

```
#include <chrono>
#include <sys/types.h>
#include <sys/stat.h>
#include <dirent.h>
#include <string>
#include <unistd.h>    <----   access函数在这个头文件中


int FileUtil::check_dir(const char* file_name){
	if (0 == access(file_name,0)) {//目录存在
		return 0;
	} else{
		if (0 == mkdir(file_name,777)) {
			return 0;
		}
		else {
			return 1;
		}
	}
}



```


```
  // FILE* file = fopen("/storage/emulated/0/hello.txt","w+");
  // FILE* file = fopen("/data/data/org.ros2.examples.android.talker/hello.txt","w+");

  // if (file != NULL) {
  //     fputs("sdkfjslkdjflskjdflksjdf", file);
  //     fflush(file);
  //     fclose(file);
  // }
  // else
  // {
  //   LOGE("open failed ...");
  // }
```
