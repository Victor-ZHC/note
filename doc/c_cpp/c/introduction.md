# Introduction

## 编译与链接
```
#include <stdio.h>

int main(void) {
    printf("Hello World!\n");
    return 0;
}
```
编译器编译过程包括三个步骤：

1. 预处理：程序被交给 __预处理器（Preprocessor）__ 。预处理器用于执行以#开头的指令，预处理指令用于对代码内容进行修改。
2. 编译：修改后的代码由 __编译器（Compiler）__ 处理。编译器讲代码编译为机器指令。
3. 链接： __连接器（Linker）__ 将机器指令与其他附加代码进行整合，最终产生可执行文件。

* 目前GCC是最流行的C语言编译器，编译C文件可使用`gcc -o output.o file.c`命令。 