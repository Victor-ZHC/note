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

[返回目录](../CONTENTS.md)