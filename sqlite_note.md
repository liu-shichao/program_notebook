### 1.sqlite在linux版本下的动态库编译

```
gcc -fPIC -shared -O3 -lpthread -ldl -lm -o libsqlite3.so sqlite3.c
```


```
 gcc -fPIC -shared -I/home/liushichao/work/AvatarEditor/third_party_library/sqlite3 -L/home/liushichao/work/AvatarEditor/third_party_library/sqlite3 -lsqlite3 -o libsqlite3pp.so sqlite3pp.cpp 

 gcc shell.c sqlite3.c -lpthread -ldl -lm -o sqlite3
 
 gcc -fPIC -shared -O3 -lpthread -ldl -lm -o libsqlite3.so sqlite3.c

```
