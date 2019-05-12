# 指针

## 指针变量
指针是存储内存地址的变量，指针的声明与普通变量的声明基本一致，但必须在变量名前放置`*`：
```
int *p;     // p仅能指向整数类型
double *q;  // q仅能指向double类型
char *c;    // c仅能指向字符类型
```

## 取地址运算符和间接寻址运算符
```
\\ &取地址运算符，获取变量的地址
\\ *间接寻址运算符，通过指针获取指针保存内存地址中的值
int i, *p;
p = &i;
printf("%d", *p);
```

## 指针作为参数或返回值
指针作为参数可以直接对传入参数进行修改。
```
void add(int a. int b, int *sum) {
    *sum = a + b;
    return;
}

int main() {
    int a = 1, b = 2, sum;
    add(a, b, &sum);
    printf("%d", sum);
}
```

函数也可以作为指针返回。但是绝不可以返回局部变量的指针。
```
int *max(int *a, int *b) {
    return *a > *b ? a : b;
}
```

## 指针与数组
数组在逻辑上是地址连续的相同数据类型，如果使用指针指向数组头，便可通过加减来操控指针访问数组内容：
```
int a[10] = {0};
int *p;

p = &a[0];      // p指向a[0]
p += 1;         // p指向a[1]
```

数组名可以用数组的名字作为指向数组第一个元素的指针，多维数组在内存中按照顺序排列，访问多维数组a[n][m]时可以使用*(a + n * row + m)实现。

## 高级应用

### 动态分配内存
除动态数组外，还可用通过stdlib.h系统库函数进行内存动态分配：
- `malloc`：分配内存块，但是不进行初始化，可以用于动态分配字符串与数组，函数原型：`void *malloc(size_t size)`，void指针可以指向任何类型的内存。
- `calloc`：分配内存块，并对内存区域清零，函数原型：`void *calloc(size_t nmemb, size_t size)`
- `realloc`：调整之前分配的内存块大小

### 释放内存空间
malloc函数都会在堆中进行内存分配，如果使用完后没有释放该区域的内存，会导致内存泄漏。`void free(void *p)`函数用于释放指针指向的内存区域。被free过的指针将不指向任何内存空间，称为**悬空指针**。

### ->运算符
通常使用指针指向某一结构体，当需要获取其成员时，需要使用`(*node).value`，为了简洁表示，可以使用`->`运算符，`node -> value <==> (*node).value`

### 指向指针的指针
在使用链式结构时，通常使用指针的指针进行操作。

### 指向函数的指针
```
double integrate(double (*f)(double), double a, double b);  // (*f)就是函数的指针，其作为函数的参数之一

double integrate(double f(double), double a, double b);     // 另一种写法
```
C语言将函数指针与指向数据的指针看做一致，这样就可以将函数指针存储在变量中（常见的是结构体中，很像面向对象）。

[返回目录](../CONTENTS.md)