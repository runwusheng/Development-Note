Shell脚本学习
---

### 创建Shell
* `touch <name>.sh`或者`vim <name>.sh`
* `open -e <name>.sh`

### 创建可双击运行的shell脚本
* `touch name` 无后缀
* `vim name` 编辑文件，#!/bin/sh开头
* 在文件目录下执行`chmod +x <name>`或`chmod 777 <name>`使得name文件变成可双击运行的脚本

### 运行Shell
* 方法1：在Mac的终端中，cd到shell的目录，然后执行`./<file.sh>`就可以运行对应的shell脚本，**如果出现`Permission denied`，可使用`chmod +x <file.sh>`或者` chmod 777 <file.sh>`来获得权限后，再重试**`./<file.sh>`即可
* 方法2：把对应的shell脚本拖动到终端中，回车执行
* 方法3：把后缀修改为`.command`，再双击运行

### 遇到的坑
1. `Permission denied`权限问题
2. Mac中Shell脚本输入双引号和单引号自动转换样式的问题，需要在修改**[打开键盘偏好设置]--[键盘]--[文本]--[双引号样式]->>选择最下面的样式**

###参考
* [Shell脚本编程30分钟入门](https://github.com/qinjx/30min_guides/blob/master/shell.md)