### 18.libstdc++/libc++

```
gcc配套的 libstdc++
llvm/clang++ 配套的 libc++

libstdc++包含两个库   libstdc++.so(接口层) 和 libsupc++.so(实现层) 
libc++包含两个库 libc++.so(接口层) libc++abi.so(实现层)

libstdc++的头文件位置 /usr/include/c++/5.4/  其中5.4位gcc编译器的版本号
libc++头文件的位置 /usr/include/c++/v1/

配置编译选项:【注意】这个是配置选择头文件的
-stdlib=libc++ 
-stdlib=libstdc++


通过cmake配置
set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -stdlib=libc++ -lc++ -lc++abi")

```



### 17.虚析构的作用

```
1.通过父类指针释放所指向的子类。

class Animal {
  vitual ~Animal() {
    std::cout << "delete animal.." << std::endl;
  }
}

class Dog : public Animal {
  ~Dog() {
    std::cout << "delete dog..." << std::endl;
  };
};

Animal* animal = new Dog();

delete animal;

```
如上执行会输出

```
delete dog...
delete animal..
```

如果去掉了vitual修饰~Animal()，则会只输出如下


```
delete animal..
```

因为父类的构造函数和析构函数不能被子类继承，但是会形成多态，

所以当父类定义成虚析构函数的时候，会先动态调用子类的析构函数，

然后由于delete的机制，会接着调用父类的析构函数



### 16.待查。。。

```
std::atomic_bool                             shutdownFlag_;
while (!shutdownFlag_.load(std::memory_order_acquire)) {

}

```

### 15.同名的头文件
如果搜索路径中包含两个同名的头文件，这时候只会包含第一个搜索到的头文件。示例如下

```
目录结构

cpptest
|
|---build
|
|---include_1
|   |
|   |---same_name.hpp
|
|---include_2
|   |
|   |---same_name.hpp
|
|---main.cpp
|
|---CMakeLists.txt
```

``include_1/same_name.hpp`` 中内容如下

```
struct cat{
  int age;
};

```

``include_2/same_name.hpp`` 中内容如下

```
struct dog{
  int age;
};

```

``CMakeLists.txt``内容如下

```
project(demo)
set(CMAKE_CXX_STANDARD 11)

add_executable(
  ${PROJECT_NAME}
  main.cpp)

target_include_directories(
  ${PROJECT_NAME}
  PUBLIC
  include_2
  include_1
)
```

``main.cpp``内容如下

```
#include <iostream>
using namespace std;
#include "same_name.hpp"

int main(int argc, char* argv[]) {
  cat c;
  c.age = 1;
  dog d;
  d.age = 2;
  cout << d.age << endl;
}
```

这时候编译会报错如下

```
/Users/liushichao/Exercise/cpp/test_cpp/main.cpp:6:3: error: unknown type name 'cat'
```

调整``CMakeLists.txt``内容如下

```
project(demo)
set(CMAKE_CXX_STANDARD 11)

add_executable(
  ${PROJECT_NAME}
  main.cpp)

target_include_directories(
  ${PROJECT_NAME}
  PUBLIC
  include_1
  include_2
)
```

这时候编译会报错如下

```
/Users/liushichao/Exercise/cpp/test_cpp/main.cpp:8:3: error: unknown type name 'dog'
```

调整``CMakeLists.txt``内容如下

```
project(demo)
set(CMAKE_CXX_STANDARD 11)

add_executable(
  ${PROJECT_NAME}
  main.cpp)

target_include_directories(
  ${PROJECT_NAME}
  PUBLIC
)
```

``main.cpp``内容如下

```
#include <iostream>
using namespace std;
#include "include_1/same_name.hpp"
#include "include_2/same_name.hpp"

int main(int argc, char* argv[]) {
  cat c;
  c.age = 1;
  dog d;
  d.age = 2;
  cout << d.age << endl;

}
```

这样就可以运行成功了。



### 14.可变参数数模板 

1.递归展开参数包
```
#include <iostream>
using namespace std;

std::string operator""_s (const char* orign) {

  return  orign;
}

template <typename T>
T sum(T head) {
  return head;
}

template <typename T, typename... Types> 
T sum(T head, Types... args) {
  cout << sizeof...(args) << endl;
  return head + sum<T>(args...);
}

int main(int argc, char* argv[]) {
  cout << sum(1, 2, 3, 4, 5) << endl;
}
```




### 13.c++操作符 / operators

c++ 11 引入了新的操作夫，用户定义字面量操作符，https://en.cppreference.com/w/cpp/language/user_literal

C++ divides the operators into the following groups:

```
Arithmetic operators
Assignment operators
Comparison operators
Logical operators
Bitwise operators
```

### 12.cpp文件中编写模板的定义

参考：

https://stackoverflow.com/a/115735

https://www.codeproject.com/Articles/48575/How-to-Define-a-Template-Class-in-a-h-File-and-Imp

```
//mstack.hpp
template<typename T>
class mstack{
 void push(const T& e);
};
```

```
//mstack.cpp
template<typename T>
void mstack<T>::push(const T& e) {
 data_.push_back(e);
}

//important!!!
// this func is no need to be call.
void testxxx() {
 mstack<int> ms;
 ms.push(1);
}
```
```
//client.cpp

void main() {
 mstack<int> m_c_s;
 m_c_s.push(2334);
}

```



### 11.类中的const成员函数

参考： c++ primer 5 中文版 p231

成员函数的参数列表后面紧跟的const关键字是修饰隐式的this指针的。是顶层指针（参考下边的10顶层const的介绍），表明this是指向常量对象的，const成员函数中的 this 指向的值不能修改。const 的对象上不能调用非const成员函数，所以定义成const的成员函数调用起来更灵活。


### 10.顶层const与底层const

参考：c++ primer 5 中文版 p57

这个是针对指针的，因为指针本身也是对象，所以const修饰指针的变量的时候可能产生歧义，一个是指针变量是常量不可变，另一种情况是指针指向的是常量，这样指针变量本身是可以修改的。

为了区分这两种情况，引入了顶层const和底层const两种类型，

```
 p  <--- p是指向i的指针，如果p是const的话，就叫顶层const，顶层const的写法   int* const p = i; ,const 直接修饰的p，
 
 |
 v

 i  <--- 如果i 是const的话，就是底层const， 底层const的写法 ： const int * p = i; ,const 直接修饰的是int，代表指向的是常量的int类型


```


### 9.std::unordered_map 查找指定key是否存在

使用``count(key)``方法，如果key存在，返回1，如果不存在，返回0



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
