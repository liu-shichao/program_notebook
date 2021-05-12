连接库编译的时候不要指定绝对路径，指定绝对路径可能在运行的时候找不到库文件

```
gcc -o demo /usr/lib/libceshi.so hello.o  #不要这样写，这样写放在别处运行可能找不到库文件
```

```
gcc -o demo -L/usr/lib -lceshi  #这样写通用性比较好
```
