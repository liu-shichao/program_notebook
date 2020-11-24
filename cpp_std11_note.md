
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
