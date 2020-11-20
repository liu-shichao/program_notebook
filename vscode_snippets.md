
自定义的代码段，可以快速创建模板

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
