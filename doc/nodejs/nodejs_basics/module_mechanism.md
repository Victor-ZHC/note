# 模块机制

## CommonJS的模块规范

### 模块引用
使用require方法导入模块
```
var math = require('math');
```

### 模块定义
使用exports方法导出模块的方法或者变量
```
exports.add = function() {
    //方法体
}
```

### 模块标识
传递给require方法的参数，本质是字符串，以. 、.. 开头的相对路径或绝对路径

## Node的模块实现
主要经历三个步骤：路径分析，文件定位，编译执行  

无论是核心模块（二进制执行文件，Node进程启动时直接加载进内存）还是文件模块（运行时动态加载），对相同模块的二次加载都一律采用缓存优先的方式

### 模块标识符分析
* 核心模块（如http、fs、path）
    * 加载速度最快，已经被编译为二进制代码
* 路径形式的文件模块
* 自定义模块
    * 当前文件目录下的node_modules目录
    * 父目录下的node_modules目录
    * 沿路径向上逐级递归，直到根目录下的node_modules目录
* 文件定位
    * 文件扩展名分析：按照.js、.json、.node的次序一次查找
    * 目录分析和包：当标识符分析过程中得到的是一个目录，那么node将把目录当做包处理，首先解析目录中的package.json文件，其次查看index（.js、.json、.node）文件

### 模块编译
* .js文件
    * 文件被包装为
    ```
    (function (exports, require, modle, __filename, __dirname) {
        //文件内容
    })
    ```
    * 包装之后的代码会通过vm的runInThisContext()方法执行
* .node文件
    * 这些文件是用C/C++写的扩展文件
    * 调用process.dlopen()方法加载和执行
* .json文件
    * 使用JSON.parse()方法得到对象
* 其他文件
    * 按照.js文件解析

[返回目录](../CONTENTS.md)