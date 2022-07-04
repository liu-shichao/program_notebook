连接库编译的时候不要指定绝对路径，指定绝对路径可能在运行的时候找不到库文件

```
gcc -o demo /usr/lib/libceshi.so hello.o  #不要这样写，这样写放在别处运行可能找不到库文件
```

```
gcc -o demo -L/usr/lib -lceshi  #这样写通用性比较好
```


```
 绝对路径虽然申请设置环境变量步骤，但是缺陷也是致命的，这个so必须放在绝对路径下，不能放到其他地方，这样给部署带来很大麻烦。所以应该禁止使用绝对路径链接so。
```


生成动态库：

参考：https://www.cnblogs.com/jiqingwu/p/linux_dynamic_lib_create.html

```
gcc -fPIC -shared -o libmax.so max.c
```

实际上上述过程分为编译和链接两步， -fPIC是编译选项，PIC是 Position Independent Code 的缩写，表示要生成位置无关的代码，这是动态库需要的特性； -shared是链接选项，告诉gcc生成动态库而不是可执行文件。

等同于

```
gcc -c -fPIC max.c
gcc -shared -o libmax.so max.o
```
