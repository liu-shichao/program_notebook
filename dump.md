```
cmake_minimum_required(VERSION 3.18)
project(prj)
add_subdirectory(src/lib)
add_subdirectory(src/config)
aux_source_directory(src/src source_src)
add_executable(hlo ${source_src})
include_directories(include .)

target_link_libraries(hlo tstlib)

set(CMAKE_INSTALL_PREFIX ../install)
#install(TARGETS testlib DESTINATION lib)
install(TARGETS hlo DESTINATION bin)
install(FILES include/lib/libcpp.hpp DESTINATION include)
```
