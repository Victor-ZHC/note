# 编写大型程序

## 源文件
C程序可以分割成任意数量的源文件，源文件的扩展名为.c。

## 头文件
源文件之间无法直接相互调用，这时，需要使用`#include`指令将需要共享的函数原型、宏定义以及类型定义等信息添加到源文件中。保存函数原型、宏定义以及类型定义的文件被称为头文件，通常使用.h作为后缀。

### #include指令
存在三种写法：
- `#include<文件名>`：用于属于C语言库内的头文件
- `#include "文件名"`：用于所有其他的头文件
- `#include 记号`：可以使用记号代替文件名，这样可以按条件进行文件包含

文件名尽量不要写绝对路径名，这样很难进行移植。

若源文件包含头文件两次，那么可能产生编译错误，可以使用`#ifdef`和`#endif`指令来封闭文件内容：
```
#ifndef BOOLEAN_H
#define BOOLEAN_H

#define TRUE 1
#define FALSE 0
typedef int BOOL;

#endif
```

BOOLEAN_H本质并无意义，只是用于标记头文件的，避免与其他宏冲突。

## 构建多文件程序

### makefile
编译大型程序时往往需要在命令行中输入大量的源文件信息，所以出现了makefile的概念，其包含了构建程序的必要信息。通过描述文件间的依赖性来构建程序。

```
justify: justify.o word.o line.o
        gcc -o justify justify.o word.o line.o

justify.o: justify.c word.h line.h
        gcc -c justify.c

word.o: word.c word.h
        gcc -c word.c

line.o: line.c line.h
        gcc -c line.c
```

每一组称为一条规则，每条规则的第一行给出目标文件，后面是其所有以来。第二行是待执行指令。当一个文件被修改，则依赖链上所有文件将被重新编译。

[返回目录](../CONTENTS.md)