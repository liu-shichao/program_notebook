
找到编译出来的文件：

```
/Users/liushichao/workspace/ros2/ros2_android_new/ros2_android_ws/build_isolated/foonathan_memory_vendor/foo_mem-ext-prefix/src/foo_mem-ext/src/CMakeLists.txt
```

查找代码

```
# generate container_node_sizes.hpp
if(FOONATHAN_MEMORY_BUILD_TOOLS)
    add_custom_command(OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/container_node_sizes_impl.hpp
            COMMAND ${CMAKE_CROSSCOMPILING_EMULATOR} $<TARGET_FILE:foonathan_memory_node_size_debugger> --code --alignof "FOONATHAN_ALIGNOF(T)" ${CMAKE_CURRENT_BINARY_DIR}/container_node_sizes_impl.hpp
            DEPENDS foonathan_memory_node_size_debugger
            VERBATIM)
else()
    message(WARNING "cannot generate container_node_sizes_impl.hpp, node size information will be unavailable")
    file(WRITE  ${CMAKE_CURRENT_BINARY_DIR}/container_node_sizes_impl.hpp "#define FOONATHAN_MEMORY_NO_NODE_SIZE")
endif()

```
改为如下

```

MESSAGE("==================================================")
MESSAGE("==================================================")
MESSAGE("==================================================")
MESSAGE("==================================================")
MESSAGE("CMAKE_CURRENT_BINARY_DIR : ${CMAKE_CURRENT_BINARY_DIR}/container_node_sizes_impl.hpp")
MESSAGE("==================================================")
MESSAGE("==================================================")
MESSAGE("==================================================")
MESSAGE("==================================================")

# generate container_node_sizes.hpp
#if(FOONATHAN_MEMORY_BUILD_TOOLS)
#    add_custom_command(OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/container_node_sizes_impl.hpp
#            COMMAND ${CMAKE_CROSSCOMPILING_EMULATOR} $<TARGET_FILE:foonathan_memory_node_size_debugger> --code --alignof "FOONATHAN_ALIGNOF(T)" ${CMAKE_CURRENT_BINARY_DIR}/container_node_sizes_impl.hpp
#            DEPENDS foonathan_memory_node_size_debugger
#            VERBATIM)
#else()
#    message(WARNING "cannot generate container_node_sizes_impl.hpp, node size information will be unavailable")
#    file(WRITE  ${CMAKE_CURRENT_BINARY_DIR}/container_node_sizes_impl.hpp "#define FOONATHAN_MEMORY_NO_NODE_SIZE")
#endif()

```
