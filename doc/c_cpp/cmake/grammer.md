# 语法

## 基本语法规则
1. 变量使用`${}`方式取值，但是在IF控制语句中是直接使用变量名，
2. 指令(参数 1 参数 2 ...)参数使用括弧括起，参数之间使用空格或分号分开，
    > `ADD_EXECUTABLE(hello main.c func.c)`
    >
    > `ADD_EXECUTABLE(hello main.c;func.c)`
3. 指令是大小写无关的，参数和变量是大小写相关的。但推荐全部使用大写指令。

## 指令
### project
#### 语法
`PROJECT(projectnema [CXX] [C] [Java])`
#### 作用
指定工程名和工程语言，并隐式定义了两个全局变量：`<projectname>_SOURCE_DIR`和`<projectname>_BINARY_DIR`。同时cmake系统也帮助我们预定义了 PROJECT_BINARY_DIR 和 PROJECT_SOURCE_DIR变量，他们的值分别跟前者一致。

### set
#### 语法
`SET(VAR [VALUE] [CACHE TYPE DOCSTRING [FORCE]])`
#### 作用
显式的定义变量。

对于单个文件，可以使用`SET(SRC_LIST main.c)`，如果有多个源文件，也可以定义成：`SET(SRC_LIST main.c t1.c t2.c)`。

### message
#### 语法
`MESSAGE([SEND_ERROR | STATUS | FATAL_ERROR] "message to display" ...)`
#### 作用
向终端输出用户定义的信息。包含三种类型：
- `SEND_ERROR`：产生错误，生成过程被跳过，
- `SATUS`：输出前缀为`-`的信息，
- `FATAL_ERROR`：立即终止所有cmake过程。

### add_executable
#### 语法
`ADD_EXECUTABLE(executablename ${SRC_LIST})`
#### 作用
生成一个文件名为`executablename`的可执行文件，相关的源文件是`SRC_LIST`中定义的源文件列表。

也可以忽略掉`SRC_LIST`列表中的源文件后缀，比如可以写成`ADD_EXECUTABLE(t1 main)`，cmake会自动的在本目录查找main.c或者main.cpp等，但最好不要偷这个懒，以免这个目录确实存在main.c和main。

### add_subdirectory
#### 语法
`ADD_SUBDIRECTORY(source_dir [binary_dir] [EXCLUDE_FROM_ALL])` 
#### 作用
这个指令用于向当前工程添加存放源文件的子目录，并可以指定中间二进制和目标二进制存放的位置。`EXCLUDE_FROM_ALL`参数的含义是将这个目录从编译过程中排除。

### install(TARGETS)
#### 语法
```
INSTALL(TARGETS targets...
    [[ARCHIVE|LIBRARY|RUNTIME]
        [DESTINATION <dir>]
        [PERMISSIONS permissions...]
        [CONFIGURATIONS [Debug|Release|...]]
        [COMPONENT <component>]
        [OPTIONAL]
    ] 
    [...]
)
```
#### 用法
安装的内容可以包括目标二进制、动态库、静态库。

参数中的`TARGETS`后面跟的就是我们通过`ADD_EXECUTABLE`或者`ADD_LIBRARY`定义的目标文件，可能是可执行二进制、动态库、静态库。目标类型也就相对应的有三种：
- `ARCHIVE`：特指静态库，
- `LIBRARY`：特指动态库，
- `RUNTIME`：特指可执行目标二进制。

`DESTINATION`定义了安装的路径，如果路径以/开头，那么指的是绝对路径，这时候`CMAKE_INSTALL_PREFIX`将无效。

例：
```
/**
*   可执行二进制myrun安装到 ${CMAKE_INSTALL_PREFIX}/bin 目录
*   动态库libmylib安装到 ${CMAKE_INSTALL_PREFIX}/lib 目录
*   静态库libmystaticlib安装到 ${CMAKE_INSTALL_PREFIX}/libstatic 目录
*/
INSTALL(TARGETS myrun mylib mystaticlib
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION libstatic
)
```