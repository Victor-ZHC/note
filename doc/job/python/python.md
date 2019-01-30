# Python
## 基础知识
### 数字和表达式
* ```//```表示整除，```1 // 2 = 0```
* ```**```表示幂（乘方），```2 ** 3 = 8```，等价于```pow()```函数
### 长整数
* 表示：数字末尾加上```L```

### 获取用户输入
```
x = input("x: ")
y = input("y: ")
print(int(x) * int(y))
获取x和y，输出x*y的值
```
### 模块
* 方式1：导入模块，并调用其函数，例：
```
import math
math.sqrt(4)
```
* 方式2：from模块import函数，直接使用函数，不需要模块名作为函数
```
from math import sqrt
sqrt(4)
```
* 注：复数处理相关的模块为：cmath

### 函数
* ```str()```将数值转换为字符串

## 列表和元组
* Python中容器包含：序列（例如：列表、元组）和映射（例如：字典）等，而集合容器类型均不属于两者
* Python有6种内建```序列```：列表、元组、字符串、Unicode字符串、buffer对象、xrange对象
* 列表和元组的主要区别：列表可以修改，元组不能，因此元组可以作为字典的键
* 列表示例：
```
[['Edward', 12], ['John', 10]]
```

### 通用序列操作
* 索引
```
>>> greeting = 'hello'
>>> greeting[0]
'h'
```
* 分片
```
>>> numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> numbers[7:10]
[8, 9, 10]
等价于：
>>> numbers[-3:]
```
获取整个序列：
```
>>> numbers[:]
```
分片步长：
```
>>> numbers[0:10:2]
[1, 3, 5, 7, 9]
```
* 加
加运算符连接序列：
```
>>> [1, 2, 3] + [4, 5, 6]
[1, 2, 3, 4, 5, 6]
```
* 乘
初始化一个长度为5的列表：
```
>>> sequence = [None] * 5
>>> sequence
[None, None, None, None, None]
```
* 成员资格
检查用户名和PIN码：
```
database = [['victor', 1], ['seni', '4321']]
if ['seni', '4321'] in database:
    print('Success')
```
* 长度、最小值、最大值  
函数**len(), min(), max()**，返回序列中包含的元素数量、最小值和最大值

### 列表-可变序列
* 列表操作
1. 删除元素，```del```语句：
```
>>> del database[1]
```
2. 分片赋值
```
>>> name = list['Perl']
>>> name[1:] = list('ython')
>>> name
['P', 'y', 't', 'h', 'o', 'n']
```
分片语句可以插入新元素
```
>>> numbers = [1, 5]
>>> numbers[1:1] = [2, 3, 4]
>>> numbers
[1, 2, 3, 4, 5]
```
分片语句可以删除新元素
```
>>> numbers
[1, 2, 3, 4, 5]
>>> numbers[1:4] = []
>>> numbers
[1, 5]
```
3. 列表方法  
**append()**，在列表末尾追加新的对象：lst.append(4)  
**count()**，统计某个元素在列表中出现的次数：lst.count(1)  
**extend()**，在末尾一次性追加另一个序列中的多个值：lst1.extend(lst2)  
**index()**，从列表中找出某个值第一个匹配项的索引位置：lst.index('who')  
**insert()**，将对象插入列表中：lst.insert(3, 'four')  
**pop()**，移除列表中的最后一个元素，并返回该元素的值：lst.pop()  
**remove()**，移除列表中某个值的第一个匹配项：lst.remove('be')  
**reverse()**，将列表中元素反向存放：x.reverse()  
**sort()**，在原位置对列表进行排序：lst.sort()，sort方法提供的可选参数：cmp,key和reverse，例：
```
根据元素的长度进行排序，使用len作为键函数：
>>> x = ['aardvark', 'abalone', 'acme', 'add', 'aerate']
>>> x.sort(key=len)
>>> x
['add', 'acme', 'aerate', 'abalone', 'aardvark']
```
反向排序：
```
lst.sort(reverse=True)
```

### 元组-不可变序列
1. 元组创建  
用逗号分隔值，则创建
```
>>> 1, 2, 3
(1, 2, 3)
```
2. tuple函数  
以一个序列为参数，并把它转换为元组

## 字符串  
* 标准序列操作对字符串完全适用
* 字符串不可变
* 字符串格式化
```
模板字符串：
>>> from string import Template
>>> s = Template('$x, glorious $x!')
>>> s.substitute(x='slurm')
'slurm, glorious slurm!'
```
### 字符串方法
**find()**，返回子串所在位置的最左端索引：str.find('Python')  
**join()**，是split的逆方法，用来连接序列中的元素，例：
```
>>> dirs = '', 'usr', 'bin', 'env'
>>> '/'.join(dirs)
'/usr/bin/env'
```
**lower()**，返回字符串的小写字母版：str.lower()  
**replace()**，替换字符串：str.replace('is', 'are')  
**split()**，将字符串分割成序列：str.split('/')  
**strip()**，去除两侧空格的字符串：str.strip()  

## 字典-json
### dict函数
* 通过其他映射或者键值对序列建立字典，例：
```
>>> items = [('name', 'Gumby'), ('age', 42)]
>>> d = dict(items)
>>> d
{'age': 42, 'name': 'Gumby'}
```
### 字典基本操作
**len(d)**，返回d中键值对的数量  
**d[k]**，返回关联到键k上的值  
**d[k]=v**，将值v关联到键k上  
**del d[k]**，删除键为k的项  
**k in d**，检查d中是否含有键为k的项

### 字典格式化
* 可以在转换说明符%后面加上键，表示在()中，后面跟上其他说明元素，例：
```
>>> phonebook{'Beth': '9102', 'Alice': '2341', 'Ceil': '3258'}
>>> "Ceil's phone number is %(Ceil)s." % phonebook
"Ceil's phone number is 3258."
```

### 字典方法
**clear()**，清除字典中的所有项：d.clear()  
**copy()**，浅拷贝  
**fromkeys()**，使用给定的键建立新的字典：
```
>>> {}.fromkeys(['name', 'age'])
{'age': None, 'name': None}
```
**get()**，访问字典：d.get('name')  
**has_key()**，检查字典中是否含有特定键：d.has_key(k)，相当于：k in d  
**items()或iteritems()**，将字典的所有项以列表形式返回，列表中每一项表示为键值对，且iteritems()返回一个迭代器对象  
**pop()**，获得给定键的值，并将相应键值对从字典中移除  
**update()**，利用一个字典更新另一个字典  
**values()或itervalues()**，返回字典中的值

## 条件、循环和其他语句
* 如果导入的两个模块都有open函数，则使用：
```
>>> from module1 import open as open1
>>> from module2 import open as open2
```

### 序列解包
* 多个赋值操作同时进行，例：
```
>>> x, y, z = 1, 2, 3
>>> print x, y, z
1, 2, 3
```
* 常见应用：
```
>>> scoundrel = {'name': 'Robin', 'girlfriend': 'Marion'}
>>> key, value = scoundrel.popitem()
>>> key
'girlfriend'
>>> value
'Marion'
```

### 条件和条件语句
* **if, else, elif**子句  
* 特殊比较运算符：is（是同一对象）、is not（不是同一对象）、in（是容器的成员）、not in（不是容器的成员）
* 布尔运算符：**and, or**
* 条件表达式：**a if b else c**
* 迭代某范围的数字，函数**range(0, 10)**，结果为：[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
* 并行迭代，**zip**：函数将两个序列压缩在一起，然后返回一个元组的列表

### 列表推导式，利用其它列表创建新列表：
```
>>> [x*x for x in range(10)]
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

## 抽象
### 创建函数
```
def hello(name):
    return 'Hello, ' + name + '!'
```
* 斐波那契数列函数：
```
def fibs(num)
    result = [0, 1]
    for i in range(num - 2):
        result.append(result[-2] + result[-1])
    return result
```

### 参数
* python函数只能修改参数变量本身
* 参数默认值
```
def hello(greeting='Hello', name='world'):
    print '%s, %s!' % (greeting, name)
打印： Hello, world!
```
* 收集参数：给函数提供任意多的参数，例：
```
def print_params(*params):
    print params
>>> print_params(1, 2, 3)
(1, 2, 3)
```

### 作用域
* 函数**vars()**：可以返回变量和所对应值的映射的不可见字典，定义为命名空间或者作用域：
```
>>> x = 1
>>> scope = vars()
>>> scope['x']
1
```

### 递归
示例：
```
def power(x, n):
    if n == 0:
        return 1
    else:
        return x * power(x, n-1)
```

## 面向对象
* 多态：一个方法的多种表现形式
* 封装：向程序中的其他部分隐藏对象的具体实现细节
* 继承

### 类
* 创建类
```
_metaclass_ = type
class Person:
    def setName(self, name):
        self.name = name
    def getName(self):
        return self.name
    def greet(self)
        print "Hello, world! I'm %s." % self.name
```

* 定义超类（类继承）
```
class SPAMFilter(Filter): # SPAMFilter是Filter的子类
    def init(self): # 重写Filter超类中的init方法
        self.blocked = ['SPAM']
```

* 构造方法
```
class FooBar:
    def _init_(self):
        self.somevar = 42
>>> f = FooBar()
>>> f.somevar
42        
```

* 类继承super函数
```
_metaclass_ = type # super函数只在新式类中起作用
class Bird:
    def _init_(self):
        self.hungry = True
    def eat(self):
        if self.hungry:
            print 'Aaaah...'
            self.hungry = False
        else:
            print 'No, thanks!'
class SongBird(Bird):
    def _init_(self):
        super(SongBird, self)._init_()
        self.sound = 'Squawk!'
    def sing(self):
        print self.sound
>>> sb = SongBird()
>>> sb.sing()
Squawk!
>>> sb.eat()
Aaaah...
>>> sb.eat()
No, thanks!
```

* property()函数
```
_metaclass_ = type
class Rectangle:
    def _init_(self):
        self.width = 0
        self.height = 0
    def setSize(self, size):
        self.width, self.height = size
    def getSize(self):
        return self.width, self.height
    size = property(getSize, setSize)
>>> r = Rectangle()
>>> r.width = 10
>>> r.height = 5
>>> r.size
(10, 5)
>>> r.size = 150, 100
>>> r.width
150          
```

### 异常
* 内建异常  

|类名|描述|
|-----------|:---------:|
|Exception|所有异常的基类|
|AttributeError|特性引用或赋值失败时引发|
|IOError|打开文件等引发|
|IndexError|使用序列中不存在的索引引发|
|KeyError|使用映射中不存在的键引发|
|NameError|找不到名字（变量）时引发|
|SyntaxError|代码为错误形式时引发|
|TypeError|内建操作或者函数应用于错误类型的对象时引发|
|ValueError|内建操作或者函数应用于正确类型的对象，但该对象使用不合适的值引发|
|ZeroDivisionError|除法或者模除操作的第二个参数为0时引发|

* 捕捉异常  
错误处理器：try/except
```
try:
    x = input('Enter the first number: ')
    y = input('Enter the second number: ')

    print x/y
expect (ZeroDivisionError, TypeError, NameError):
    print 'Your numbers were bogus ...'
```

* 引发异常
调用：raise语句

* 异常清理后
```
try:
    1/0
except NameError:
    print "Unknown variable"
else:
    print "That went well!"
finally:
    print "Cleaning up."
```

[返回目录](../CONTENTS.md)