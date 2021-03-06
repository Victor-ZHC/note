# Vim

## 常用快捷键
### 基本
|按键|功能|
|:---|:---|
|`ESC`|命令模式|
|`:`|末行模式|
|`:q`|退出|
|`:q!`|强制退出|
|`:w`|保存|
|`:w new_name`|另存为|
|`:wq`|保存并退出|
|`:set nu`|设置行号|
|`:reg num/+`|显示寄存器内容|

### 光标移动
|按键|功能|
|:---|:---|
|`h` `←`|左移一个字符|
|`l` `→`|右移一个字符|
|`j` `↓`|下移一行|
|`k` `↑`|上移一行|
|`0` `Home`|移动光标至本行开头|
|`$` `End`|移动光标至本行末尾|
|`G`|移动到末行首|
|`nG`|移动到n行首|
|`gg`|移动到全文开头|
|`w`|向文末移动一个词|
|`W`|向文末移动一个词(以空格分隔的词)|

### 插入文本
|按键|功能|
|:---|:---|
|`i`|光标前插入|
|`a`|光标后插入|
|`o`|光标下方新建一行|
|`O`|光标上方新建一行|

### 删除文本
|按键|功能|
|:---|:---|
|`x`|删除光标处字符|
|`d0`|删至行首|
|`d$`|删至行末|
|`dd`|删除该行|
|`dgg`|删至文件开头|
|`dG`|删至文件末尾|

### 选择文本
|按键|功能|
|:---|:---|
|`v + 光标移动`|选择文本|

### 复制粘贴
|按键|功能|
|:---|:---|
|`y`|复制选中文本|
|`"+y`|复制选中文本到系统粘贴板|
|`d`|剪切选中文本|
|`p`|粘贴到光标后|
|`P`|粘贴到光标前|

### 撤销
|按键|功能|
|:---|:---|
|`u`|撤销|
|`Ctrl + r`|重做撤销的操作|

### 搜索替换
|按键|功能|
|:---|:---|
|`/ + key`|从光标位置向前搜索|
|`? + key`|从光标位置向后搜索|
|`n`|向后查找|
|`N`|向前查找|
|`:s/src/des`|替换当前行第一个src为des|
|`:s/src/des/g`|替换当前行所有src为des|
|`:%s/src/des`|替换所有行第一个src为des|
|`:%s/src/des/g`|替换所有行所有src为des|

[返回目录](../CONTENTS.md)