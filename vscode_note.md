### 3.vscode c++无法跳转到定义

问题：

1.vscode用了一段时间后，偶尔会出现跳转不到定义的问题，上边的进度条一直在动，但是就是无法跳转。

解决方法：

1.按住command + shift + x， 将没用的插件卸载掉，将c++相关的插件卸载再重装一下，然后点一下插件那里的reload，来生效。



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
			"namespace ${2:sgmm} {", 
			"",
			"",
			"",
			"",
			"}"
		],
		"description": "A cpp file template."   
	},

	"cpp include file template.":{
		"prefix": "INCLUDE", 
		"body": [
			"#ifndef ${TM_FILENAME_BASE/(.*)/${1:/upcase}_HPP/}",
			"#define ${TM_FILENAME_BASE/(.*)/${1:/upcase}_HPP/}",
			"",
			"namespace ${2:sgmm} {",    
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
