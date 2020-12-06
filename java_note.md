### 编译执行java的方法

1.新建一个java后缀的源码文件

```
touch HelloWorld.java  //这个文件名要与文件中的类名一致
```
2.编写文件中的源码

```
class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

3.编译成class文件

```
javac HelloWorld.java
```

4.执行java

```
java HelloWorld  //这里不能用java HelloWorld.class
```
