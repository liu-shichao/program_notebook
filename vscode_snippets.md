
自定义的代码段，可以快速创建模板

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
