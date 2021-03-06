# 声明

声明的格式：
`声明说明符 声明符`

声明符给出了名字，声明说明符给出了变量或函数的性质

## 声明说明符
分为3大类
- 存储类型。分为四种：auto、static、extern和register。在声明中最多可以出现一种存储类型。且必须放在第一位。
- 类型限定符。两种：const和volatile。C99还定义了restrict。
- 类型说明符。void、char、shot、int、long、float、double、signed和unsigned。这些类型可以合理组合。

## 存储类型
变量具有以下性质
- 存储期限：决定了为变量预留和内存被释放的时间。**自动存储期限**的变量在所属块被执行时获得内存单元，块终止时释放内存，变量将消失。**静态存储期限**的变量在程序运行期间占有同一个的存储单元。
- 作用域：作用域是可引用变量的那部分程序文本。分为块作用域（从声明到所在快末尾）和文件作用域（从声明到所在文件的末尾）。
- 连接：确定程序的不同部分可以共享此变量的范围。**外部链接**的变量可以被程序中的几个或全部文件共享。**内部链接**的变量只能属于单一文件。无连接的变量属于单独一个函数，且不能被共享。

默认情况下：
- 块内部声明的变量具有：自动存储期限、块作用域且无链接
- 程序最外层声明的变量具有：静态存储期限、文件作用域和外部链接

```
int i;              // 静态存储期限、文件作用域、外部链接

void f(void) {
    int j;          // 自动存储期限、块作用域、无链接
}
```

### auto存储类型
就是块内部声明的变量，所以基本不用明确指明，因为编译器会自动为块内部变量添加auto关键字。

### static存储类型
```
static int i;       // 静态存储期限、文件作用域、内部链接

void f(void) {
    static int j;   // 静态存储期限、块作用域、无链接
}
```
与auto区别
- 块内部static在程序执行前初始化一次，auto在每次出现时被初始化
- 递归时，auto都是新的内存地址，static是固定的一块内存地址
- 函数无法返回auto变量的指针，static的指针可以返回

### extern存储类型
使多个源文件共享一个变量，仅提示编译器存在这一变量，并不会为其分配内存
```
extern int i;       // 静态存储期限、文件作用域、不确定

void f(void) {
    extern int j;   // 静态存储期限、块作用域、不确定
}
```

变量的类型与之前被声明的连接类型一致

### register存储类型
将变量存储在寄存器中，与auto存储类型一致，但是访问更迅速

### 函数存储类型
```
extern int f(int i);        // 外部链接
static int g(int i);        // 内部链接
int h(int i);               // 外部链接
```

## 类型限定符
- volatile：告诉编译器该变量改变十分频繁，故编译器不能做任何优化；每次操作该值时，必须从内存中读取，也必须写到内存中，不得存入cache等地方
- const：声明变量是只读的，在许多函数声明时将形参声明为const有利于程序

## 复杂的声明
声明的理解：
- 始终从内到外读声明符。从名称开始一步一步向外解读
- 始终[]和()的优先级高于*。

`int *(*x[10])(void)`

首先，x开始读，x跟着`*`与`[]`，`[]`的等级高于`*`，所以x是数组，是指针数组，指向不带参数的函数，函数返回的是int类型的指针。


[返回目录](../CONTENTS.md)