# C++ Primer

## 基础
1. 变量和基本类型
* unsigned char 8bit，表示范围`0到255`，若超出赋值，则取该值对256求模后的值
2. C++字符串字面值由编译器自动在末尾加上空字符
3. 直接初始化效率高于复制初始化
```
直接初始化：int ival(1024);
复制初始化：int ival = 1024;
```
4. 变量定义分配存储空间，声明仅向程序表明变量类型和名字，不分配存储空间
```
extern关键字，仅声明变量而不定义
extern int i;
```
5. 默认情况下，访问级别：struct的成员为public，而class的成员private
6. 箭头操作符
```
(*p).foo; // 获得p指向对象的成员变量foo
p->foo; // 与上面等价
```

## 数组
1. sizeof：对对象求内存大小（对象数据类型的大小）
```
const char *words[] = {"apple", "banana"};
size_t st1 = sizeof(words);
size_t st2 = sizeof(char *); // 相当于string
cout << st1 << " " << st2 << endl;
size_t size = st1 / st2;
cout << size << endl;
输出：
16 8
2
```
2. strlen：求字符串的实际长度，从开始到遇到第一个\0
```
char a[10] = {'\0'};
char b[10] = "123";
cout << strlen(a) << " " << strlen(b) << endl;
cout << sizeof(a) << " " << sizeof(b) << endl;
输出：
0 3
10 10
```

## 指针和引用
1. 指针
* 可能的取值：
    * 保存一个对象的地址
    * 保存某对象后面的对象
    * 0值
2. 引用
* 绑定对象的别名，必须被初始化
```
int ival = 1024;
int &refVal = ival;
```
* 作用在引用上的所有操作实际上都是该引用绑定的对象上
* const引用是指向const对象的引用
* swap函数，交换实参的值，需要将形参定义为引用类型：
```
void swap(int &v1, int &v2) {
    int tmp = v2;
    v2 = v1;
    v1 = tmp; 
}
调用：
swap(i, j)
```
3. 举例
```
int ival = 1024;
int *pi = 0; // 初始化为0值
int *pi2 = &ival; // 初始化为ival的地址
int *pi3; // 未初始化
pi = pi2; // pi和pi2保存同一对象的地址
```
* 注：& 取地址操作符
```
// 指针 & 引用
int ival = 1024;
int &refVal = ival;
cout << refVal << endl;    
int *p = &refVal; // p保存ival的地址，*p保存值
cout << p << " " << *p << endl;
int *p2 = p;
cout << p2 << " " << *p2 << endl;

输出：
1024
0x7ffeefbff618 1024
0x7ffeefbff618 1024
```
4. 下标和指针
```
int ia[] = {0, 2, 4, 6, 8};
int *p = &ia[2]; // p指向数组下标为2的元素
int j = p[1]; // p[1]等价于*(p+1)，p[1]也就是ia[3]
int k = p[-1]; // p[-2]也就是ia[0]
```

## 顺序容器 sequential container
1. 三种顺序容器类型：
* vector（可变长数组，可扩容）
* list（双向链表）
* deque（基于双端队列，用链表连接数组）
* 注：list和deque提供了首部插入push_front和尾部插入push_back，首部删除pop_front和尾部删除pop_back

## 关联容器 associative container
1. 与顺序容器差别
* 通过key存储和读取元素
2. 三种关联容器类型：
* map
```
#include <map>
map<string,int> word_count;
word_count["Anna"] = 1;
cout << word_count["Anna"] << endl;
```
* set
* multimap和multiset
    * 键可以多次出现

## 继承
1. virtual是基类期待派生类重新定义的，派生类动态绑定，注：成员函数默认为：非虚函数
2. 构造函数后加冒号，是：成员变量的初始化
3. 在成员函数的形参后面写上=0，则成员函数为纯虚函数，包含纯虚函数的类不能被实例化
4. const修饰成员函数，防止成员变量被修改
```
virtual double net_price(std::size_t n) const {
    return n * price;
}
```

[返回目录](../CONTENTS.md)