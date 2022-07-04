### 1.sqlite在linux版本下的动态库编译

```
gcc -fPIC -shared -O3 -lpthread -ldl -lm -o libsqlite3.so sqlite3.c
```
