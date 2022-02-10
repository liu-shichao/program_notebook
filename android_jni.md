jni tool

1.android studio中创建java的类，编写好java函数，前边加上native修饰符

2.点击编译运行，会在下边这个路径下生成编译好的class文件（这个路径当你看到这个文章的时候可能已经发生变化了，需要具体的去寻找）

app/build/intermediates/javac/debug/classes

3.到这个路径下执行下边的命令，即可在当前目录下生成jni的头文件

javah -classpath . com.sogo.map.streetviewjni.StreetViewApi

4.如果想指定头文件的生成路径，需要增加一个 -d 参数，按下边的命令即可(在根目录中运行)

javah -classpath app/build/intermediates/javac/debug/classes -d app/src/main/cpp com.sogo.map.streetviewjni.StreetViewApi
