### 8.std::map有序

std::map是有序的，但是不是插入的顺序，而是按照key的值进行排序的，默认是从小到大排序，可以通过模版参数的第三个参数指定排序类型

### 7.c++计时

```
1.包含头文件
#include <chrono>

2.计时开始位置添加
std::chrono::time_point<std::chrono::high_resolution_clock> time_begin = std::chrono::high_resolution_clock::now();

3.计时结束位置添加
long long eclipse_time = std::chrono::duration_cast<std::chrono::milliseconds>(std::chrono::high_resolution_clock::now() - time_begin).count();
          
4.eclipse_time即为统计的时间，单位是ms

```




### 6.各种类型的最大最小值宏定义

包含头文件

```
#include <float.h>  //double float 需要用到这个
#include <limits.h> //int longlong long 需要用这个
```

下边是具体的最大最小值的宏定义

```
int   n1　=　INT_MIN;
int   n2　=　INT_MAX;
float　f1　=　FLT_MIN;
float　f2　=　FLT_MAX;
double　d1　=　DBL_MIN;
double　d2　=　DBL_MAX;
long ln1 =  LONG_MAX;
long ln2 =  LONG_MIN;
long long lln1 = LONG_LONG_MAX;
long long lln1 = LONG_LONG_MIN;
```



### 5.condition_variable

wait_for可以指定等待时间，用来实现定时器效果

下边的代码，可以通过condition.signal()来唤醒阻塞的线程，其他时候会到一秒钟自动唤醒，但是这种可能会有假唤醒的时候，如果要避免假唤醒，可以再传递一个函数，返回bool类型。

```
std::unique_lock<std::mutex> sleep_lock(mutex_);
condition.wait_for(sleep_lock, std::chrono::milliseconds(1000));
```





### 4.运算符优先级

```

*乘 /除

+加 -减

>大于 <小于

==等于 !=不等于

&&与 

||或

```


### 3.std::unique_lock 与 std::lock_guard的区别

unique_lock可以随时释放锁，调用unlock()

lock_guard需要等到生命周期结束后，才能自动释放锁。

```
用法示例：
    {
        std::unique_lock<std::mutex> lock_get_lane_data(mutex_lan_date_msg_);
        //lock_get_lane_data.unlock();
    }

```



### 将double转换成string时保留15位小数

```
#include <iomanip>
#include <sstream>

double ceshi = std::stod("3.123456789");
stringstream ss;
ss << std::setprecision(15) << ceshi;
std::string ceshi_str = ss.str();
cout << ceshi_str <<endl;
```

java中

```
其中String s=String.format("%.2f",d)表示小数点后任意两位小数，其中2为表示两位小数，若需要三位小数，把2改为3即可，其他同理。
```




c++ primer 5th p600

### 使用ms后缀

```
#include <chrono>
using namespace std::chrono_literals;
```

### 使用sstream输出 unsigned char存储的数字

为了节省存储空间，经常会用usigned char来存储一些数值范围比较小的数字，当用ostringstream转换成string时会出现问题，举例如下

```
unsinged char a = 10;
std::ostringstream oss;
oss << a;
cout << oss.str(); //输出换行
```

这里标准输出打印的并不是“10”，而是会换行，因为a的类型是char，所以会把a的值作为ascii码的值，转换成string，要想输出“10”，需要强转a成int类型

```
unsinged char a = 10;
std::ostringstream oss;
oss << (int)a;
cout << oss.str(); //输出10
```
