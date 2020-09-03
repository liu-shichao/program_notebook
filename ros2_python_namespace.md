ros2 用pyhton编写的节点指定命名空间的方法

1.在运行的时候用下边的命令

```
//命名空间为map_build
ros2 run instatiation_package instantiation_node --ros-args --remap __ns:=/map_build
```

2。在创建launch脚本进行参数配置
