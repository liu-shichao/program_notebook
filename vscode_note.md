### 5.vscode 远程调试传入参数的方法
vscode的debug有两种方式，一个是快速debug，这种不能传入参数，另一种是使用launch.json配置，这种可以传入参数

在进行远程调试的时候，launch.json中的有个字段一定要设置为false，否则点击运行后没有反应，就是下边这个字段：

`` "externalConsole": false, ``

### 4.vscode提示protobuffer中的类

问题描述： vscode可以正常提示c++的相关提示，但是不能提示pb.h头文件中定义的pb类中的成员函数或者变量。

问题原因：vscode默认只从当前工作空间中查找所引用的类，虽然proto转换的pb.h在工作空间中，但是pb.h依赖的protobuf的库的头文件没有在工作空间中，这样就会导致无法解析当前工作空间中的pb.h文件，所以涉及到的类中的成员函数和变量都不会提示。

解决方法：
```
1.按下 Ctrl+Shift+P
2.输入edit或者configuration，选择”C/Cpp:Edit Configurations(JSON)”
3.编辑打开的c_cpp_properties.json文件，在includePath中加入pb库所在的路径，示例如下
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "/Users/liushichao/grpc/mac_install/**",
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "macFrameworkPath": [],
            "compilerPath": "/usr/local/bin/gcc-10",
            "cStandard": "gnu17",
            "cppStandard": "gnu++14",
            "intelliSenseMode": "macos-gcc-x64"
        }
    ],
    "version": 4
}


```


### 3.vscode c++无法跳转到定义

```
问题：

1.vscode用了一段时间后，偶尔会出现跳转不到定义的问题，上边的进度条一直在动，但是就是无法跳转。

解决方法：

1.按住command + shift + x， 将没用的插件卸载掉，将c++相关的插件卸载再重装一下，然后点一下插件那里的reload，来生效。

```


### 2.vscode C++ / Cpp自动补全功能有些成员不提示的解决方法

1. 卸载``ms-vscode.cpptools``插件，重新安装

2. 按``command + p``输入``settings.json``，打开配置文件

3. 在配置文件中添加如下代码，开启智能提示

```
 "editor.minimap.enabled": true,
    "C_Cpp.autocomplete": "Default",
    "[cpp]": {
        "editor.quickSuggestions": true
    },
    "[c]": {
        "editor.quickSuggestions": true
    }
}
```


### 1.自定义的代码段，可以快速创建模板

官方文档：https://code.visualstudio.com/docs/editor/userdefinedsnippets#_assign-keybindings-to-snippets

vscode中输入command + p，再输入条中输入cpp.json,将下面的代码粘贴进去，在cpp文件中可以直接输入cpp，在智能提示里选CPP，图标是个方块，按回车就好了，在头文件可以找INCLUDE提示。

```
{
	"cpp source file template.":{
		"prefix": "CPP",    
		"body": [
			"#include \"${TM_FILENAME_BASE}.hpp\"",
			"", //空行
			"namespace ${1:xiaobing_virtual_synthesis} {", 
			"",
			"",
			"",
			"",
			"}"
		],
		"description": "A cpp file template."   
	},

	"cpp include file template.":{
		"prefix": "HPP", 
		"body": [
			"#ifndef ${TM_FILENAME_BASE/(.*)/_${1:/upcase}_HPP_/}",
			"#define ${TM_FILENAME_BASE/(.*)/_${1:/upcase}_HPP_/}",
			"",
			"namespace xiaobing_virtual_synthesis {",    
			"", //空行
			"class ${1:${TM_FILENAME_BASE/(.*)/${1:/capitalize}/}}", 
			"{",
			"public:",
			"    ${1:${TM_FILENAME_BASE/(.*)/${1:/capitalize}/}}();",
			"    ~${1:${TM_FILENAME_BASE/(.*)/${1:/capitalize}/}}();",
			"",
			"private:",
			"",
			"};//class",
			"",
			"",
			"",
			"${1:${TM_FILENAME_BASE/(.*)/${1:/capitalize}/}}::${1:${TM_FILENAME_BASE/(.*)/${1:/capitalize}/}}()",
			"{",
			"    $0",
			"}",
			"",
			"${1:${TM_FILENAME_BASE/(.*)/${1:/capitalize}/}}::~${1:${TM_FILENAME_BASE/(.*)/${1:/capitalize}/}}()",
			"{",
			"",
			"}",
			"",
			"",
			"",
			"}//namespace",
			"",
			"#endif"
		],
		"description": "A hpp file template."   
	}
}
```
