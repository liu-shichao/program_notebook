## c++计时

```
1.包含头文件
#include <chrono>

2.计时开始位置添加
std::chrono::time_point<std::chrono::high_resolution_clock> time_begin = std::chrono::high_resolution_clock::now();

3.计时结束位置添加
long long eclipse_time = std::chrono::duration_cast<std::chrono::milliseconds>(std::chrono::high_resolution_clock::now() - time_begin).count();
          
4.eclipse_time即为统计的时间，单位是ms

```
