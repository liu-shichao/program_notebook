# cmake+NDK命令行编译cpp

1.cmake-toolchains

cmake调用用一系列的工具（工具链），来进行代码的编译，库的链接，以及最后的大包生成。在执行主机编译时（在电脑上编译本机运行的程序），cmake会自动识别本机的工具链，进行构建程序，当为其他设备（例如手机或者开发板）编译程序时，需要提供一个工具链文件的信息，用指定的工具链来进行构建程序，也就是交叉编译。