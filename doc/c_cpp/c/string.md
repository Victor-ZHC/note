# 字符串

## 字符串字面量
使用一对双引号括起来的字符序列。

"Hello World"

若字符串太长而无法放在一行内，可用`\`字符结尾（本质是`\`加回车符），但是新行的字符串必须从行开头开始，破坏了程序的易读性，所以通常使用两字符串拼接（"str1" "str2"）。

## 字符串变量
C语言使用字符数组存储字符串字面量，并使用`\0`字符作为结尾。
```
char str[12] = "Hello World";
char *p = "Hello World";
```

由于指针可以指向数组，故指针可以指向一个字符串，但是这两种声明方式会有以下区别：
- str[]可以任意修改存储在数组中的字符；p在试图修改字符串时将出现未定义行为。
- str是数组名；p是变量，可以在程序执行时指向其他字符串。 

## 字符串库

### strcpy函数
`char *strcpy(char *s1, const char *s2);`
将字符串s2复制给字符串s1。

### strlen函数
`size_t strlen(const char *s);`
返回字符串长度。

### strcat函数
`char *strcat(char *s1, const char *s2);`
将s2的内容追加到s1末尾，并返回s1。

### strcmp函数
`int strcmp(const char *s1, const char *s2);`
比较字符串s1与s2，跟进s1小于、等于或大于s2，返回一个小于、等于或大于0的数。

s1小于s2满足下列任意条件：
- s1与s2在前i个字符一致，s1的第i+1个字符小于s2的第i+1个字符
- s1与s2的所有字符一致，但是s1比s2短

## 字符串数组

char str[N][M] = {
    "str1",
    "str2",
    "str3",
    "str4",
    "str5"
}

这种方式会浪费内存，通常按照以下方式声明：

char *str[N] = {
    "str1",
    "str2",
    "str3",
    "str4",
    "str5"
}

### 命令行参数
命令行运行标准C程序的main函数存在两个参数，这两个参数分别是`argc`与`argv`:

```
int main(int argc, char *argv[]) {

}
```

- argc：命令行输入的参数个数
- argv：参数按序组成的字符串数组

其中第一个参数是程序名称，第argv[argc]个元素是一个空指针。

[返回目录](../CONTENTS.md)