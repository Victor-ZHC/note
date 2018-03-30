# Java程序员面试笔试
## 第四章
1. clone方法的作用
* java处理基本类型都是按值传递，其他类型都是按引用传递
* clone()是Object类的方法，返回对象的复制
2. 多态的实现机制
* 重载overload
* 重写override
3. getClass() P74
* Object类中final native的方法，实际调用都是Object的getClass()
4. finally P78
* 资源的释放，如：打开文件的关闭
5. static P82
* 内部类才能被定义为static
* 应用：单例模式
6. 装饰者模式
* 应用：java IO流
7. Object类的hashCode()
* 将内存中对象的地址映射为一个int
8. 数据库JDBC加载驱动
```
String driver = "jdbc:mysql://localhost:3306/Test";
Class.forName(driver);
```
* 反射机制，向DriverManager注册该Driver
* 下面两者等价，后者可用于配置文件
```
Test t = new Test();
Test t = (Test)(Class.forName("Test")).newInstance();
```