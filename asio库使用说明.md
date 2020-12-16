### 发送post请求示例


使用postman请求示例:
```
[post]
http://1.2.3.37:12000/location_tool/ENU_to_LLA

[body][raw][json]
{
"original_point":[39.779458, 116.513864, 32],
"enu_point":[-16.244472, 23805.665270, -54.147690]
}

```
```

    try
    {
        asio::io_context io_context;
        tcp::resolver resolver(io_context);
        tcp::resolver::results_type endpoints =
        resolver.resolve("1.2.3.37", "12000");
        tcp::socket socket(io_context);
        asio::connect(socket, endpoints);
        asio::streambuf request;
        std::ostream request_stream(&request);
        std::string json = "{\"original_point\":[39.779458, 116.513864, 32],\"enu_point\":[-16.244472, 23805.665270, -54.147690]}";
        request_stream << "POST " << "/location_tool/ENU_to_LLA" << " HTTP/1.0\r\n";
        request_stream << "Host: " << "1.2.3.37:12000" << "\r\n"; 
        request_stream << "Content-Length: " << json.length() << "\r\n";
        request_stream << "Content-Type: application/x-www-form-urlencoded\r\n";
        request_stream << "Accept: */*\r\n";
        request_stream << "Connection: close\r\n\r\n";
        request_stream << json.c_str();
        asio::write(socket, request);

        for (;;)
        {
            array<char, 128> buf;
            asio::error_code error;

            size_t len = socket.read_some(asio::buffer(buf), error);
            if (error == asio::error::eof)
            break; // Connection closed cleanly by peer.
            else if (error)
            throw asio::system_error(error); // Some other error.

            std::cout.write(buf.data(), len) << endl;
            cout << "len : " << len << endl;
        }
    }
    catch (std::exception& e)
    {
        std::cerr << e.what() << std::endl;
    }


```










### 调用库
asio库是纯头文件的库，使用时只要包含头文件即可，但是要指定一个宏定义，以及指定c++的版本为11以上，具体的cmakelist如下

```
set(CMAKE_CXX_STANDARD 11)

project(log_convertor)

add_executable(
    ${PROJECT_NAME}
    src/main.cpp
)

target_include_directories(
    ${PROJECT_NAME}
    PUBLIC
    /Users/liushichao/workspace/library/rapidjson/include
    /Users/liushichao/Desktop/asio/asio/include
)
target_compile_definitions(
    ${PROJECT_NAME} 
    PUBLIC 
    ASIO_STANDALONE)


```
