### 3.glob通配符获取文件列表

```
glob.glob("./*.jpg")
获取当前目录下的jpg文件列表
```


### 2.__init__.py的作用

参考链接 https://www.cnblogs.com/lands-ljk/p/5880483.html

__init__.py 文件的作用是将文件夹变为一个Python模块,Python 中的每个模块的包中，都有__init__.py 文件。

通常__init__.py 文件为空，但是我们还可以为它增加其他的功能。我们在导入一个包时，实际上是导入了它的__init__.py文件。这样我们可以在__init__.py文件中批量导入我们所需要的模块，而不再需要一个一个的导入。

当导入模块时，解释器按照sys.path列表中的目录顺序来查找导入文件。

```
import sys
print(sys.path)
```


### 1.编译ros提示缺少em模块

python3 -m pip install empy
