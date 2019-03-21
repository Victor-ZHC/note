# 控制语句

## 选择语句

### 逻辑表达式
关系运算符（`<`、`>`、`>=`、`<=`）判等运算符（`==`、`!=`）逻辑运算符（`&&`、`||`）连接的表达式，结果返回真（1）或假（0），C语言中`==`号仅能用于基本类型上的判断，字符串判等需要使用`strcmp()`函数。

**注**：逻辑运算符拥有短路效应。

### if语句
```
if (bool) {
    /* statements */
} else if (bool) {
    /* statements */
} else {
    /* statements */
}
```

else语句总是与上一个距自己最近的if语句相匹配。

### 三元条件表达式
`s1 ? s2 : s3;`

s1成立，则s2，否则s3。

### switch语句
```
switch(表达式) {
    case 常量表达式 : /* statements */
    ...
    case 常量表达式 : /* statements */
    default : /* statements */
}
```

一旦传入表达式符合某一常量表达式会将后面所有语句执行，不要忘记在使用`break`跳出`switch`。

## 循环语句

### while语句

```
while (bool) {
    /* statements */
}
```

### do语句

```
do {
    /* statements */
} while (bool);
```

### for语句
```
for (表达式1; 表达式2; 表达式3) {   \\ 表达式2返回bool类型
    /* statements */
}
```

执行顺序：表达式1 -> 表达式2 -> 语句 -> 表达式3

### 退出循环语句

- `break`语句：吧程序控制从包含该语句的最内侧`while`，`do`、`for`或`switch`语句中转移出来。
- `continue`语句：直接将程序控制转至循环体末尾。
- `goto`语句：直接将程序跳转至程序任意位置。

```
标识符 : /* statements */

goto 标识符;
```

[返回目录](../CONTENTS.md)