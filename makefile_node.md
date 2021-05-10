### 通配符的使用

  shell中使用的通配符有: `` "*", "?", "[...]"  ``， 其中``[]``代表匹配一个字符，这个字符是``[]``内指定的，如``[xyz]``，匹配x或者y或者z， ``[0-9]``代表0到9之间的一个字符， ``[!0-9]``或者``[^0-9]``代表不是0到9内的任意字符。

  除了使用shell中的通配符外，cmake中还有一个类似``*``的符号``%``，可以用来匹配任意个字符，在规则当中使用。
  
  例如：
  
  ```
  test:test.o test1.o
    gcc -o $@ $^
  %.o:%.c
    gcc -o $@ $^
  
  ```
  这个会遍历所有.o结尾的文件，然后找到对应的.c文件，逐条执行下边的命令。
【注意：wildcard参数不要带双引号，如$(wildcard ./include/*) 不要写成 $(wildcard "./include/*")】  
  



### 变量的赋值
  
  ``x:=y``这种是一般认为的赋值，只会影响当前这行内容
  
  ``x=y``这种是递归赋值，可以理解为赋值的是引用，当y的内容发生变化后，x的内容也会跟着变

### 自动化变量
  
```
    $@ 表示规则的目标文件名   【注：规则中包含目标文件和依赖文件，如 目标文件：依赖文件 依赖文件2 依赖文件3 形式】
    $^ 表示依赖文件的列表，用空格分隔的， 这个变量会对其中的文件列表进行去重
```

### 文件搜索（VPATH 和vpath）


VPATH是搜索变量，赋值以后会在这个变量里寻找。

```
  
  VPATH := src car
  
  或者
  
  VPATH := src:car
  
```

vpath是需要指定要搜索的文件，用法如下

```
vpath test.c src car  #在src和car目录下寻找test.c文件
vpath %.c src car     #在src和car目录下查找全部的.c文件
vpath teset.c         #清除test.c的搜索目录
vpath                 #清除所有已被设置的文件搜索路径

```

### 条件分支语句

注意：条件语句只能用于控制make实际执行的Makefile文件部分，不能控制规则的shell命令执行的过程。

1.ifeq

```
ifeq ($(cc),gcc)
  libs=$(libs_for_gcc)
else
  libs=$(normal_libs)
endif
```

2.ifdef

```
bar =
foo = $(bar)
all:
ifdef foo
  @echo yes
else
  @echo no
endif

```

### 伪目标


不会创建目标文件，只是想执行这个目标下边的命令。

作用：
```
1.避免只执行命令的目标和实际存在的文件出现名字冲突
2.提高执行make时的效率
```

方法：
将目标作为特殊目标``.PHONY``的依赖，如下

```
.PHONY:clean
```

### 函数


函数的调用

```
$(<function> <arguments>)     或者  ${<function> <arguments>}
```

function是函数名，arguments是参数， 参数需要用逗号分隔，参数和函数名之间用空格分隔。


### 字符串操作函数

1.patsubst 字符串替换函数

```
$(patsubst <pattern>,<replacement>,<text>)
```

从text中查找符合模式pattern的字符用replacement进行替换,实例：

```
OBJ=$(patsubst %.c,%.o,1.c 2.c 3.c)
all:
  @echo $(OBJ)
```

输出结果：

```
1.o 2.o 3.o
```

2.sbust  字符串替换函数

```
$(subst <from>,<to>,<text>)
```

把text中的from替换成to

3.strip 去空格函数，去掉string开头和结尾的空格，并将中间的多个空格合并为一个空格

```
$(strip <string>)
```

4.findstring 查找子字符串， 查找in中的find，如果目标字符串存在，返回目标字符串，不存在返回空

```
$(findstring <find>,<in>)
```
例：

```
OBJ=$(findstring a,a b c)
all:
  @echo $(OBJ)
```
显示结果为``a``


5. filter 过滤函数， 过滤出text中符合模式pattern的字符串，可以有多个pattern，返回值为过滤后的字符串

```
$(filter <pattern>,<text>)
```

6.filter-out反过滤函数，去除符合模式pattern的字符串，返回保留的字符串

```
$(filter-out <pattern>,<text>)
```

7.sort排序函数， 将list中的单词排序（升序），返回排好序的字符串

```
$(sort <list>)
```

8.word 取单词函数，去除text中的第n的单词，返回去除的第n个单词，从1开始计数

```
OBJ=$(word 2,1.c 2.c 3.c)
all:
  @echo $(OBJ)
```
返回``2.c``


### 文件名操作函数
























