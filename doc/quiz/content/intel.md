# intel
1. String、StringBuffer和StringBuiler区别
    * 执行速度 StringBuilder>StringBuffer>String
    * String是字符串常量，StringBuilder和StringBuffer是字符串变量
    * StringBuilder线程不安全，StringBuffer线程安全
2.  多线程实现的方法
    * 四种方式
* 方式1：继承Thread类
```
public class MyThread extends Thread {  
    public void run() {  
        System.out.println("MyThread.run()");  
    }  
}  
MyThread myThread = new MyThread();  
myThread.start();
```
* 方式2：实现Runnable接口
```
public class MyThread implements Runnable {  
    public void run() {  
        System.out.println("MyThread.run()");  
    }  
}
Thread thread = new Thread(new MyThread());  
thread.start();
```
* 方式3：实现Callable接口利用FutureTask包装器
* 方式4：使用ExecutorService、Callable、Future实现有返回结果的多线程
3. 抽象类和接口
* 抽象类
```
public abstract class Demo {  
    abstract void method1();   
    void method2(){  
        //实现  
    }  
} 
```
* 接口
```
interface Demo {  
    void method1();  
    void method2();  
} 
```
* 对比

||抽象类|接口|
|-|-|-|
|方法实现|可以有默认的方法实现|完全抽象|
|实现|子类extents|类implements|
|构造器|可以有|必须无|
|与正常Java区别|不能实例化|不是类|
|访问修饰符|可以public,protected,default|仅public|
    * 抽象类可以有抽象方法和非抽象方法，但是抽象方法必须在抽象类中
    * 接口的方法必须都是抽象的
    * 类可以实现多个接口，但只能继承一个抽象类
    * java 8允许给接口添加非抽象的实现，只需要加上default关键字
4. 线程安全
* ArrayList（线程不安全）和Vector（线程安全）
    * Vector所有方法都同步synchronized了
        * synchronized实现：monitorenter和monitorexit
* HashMap（线程不安全）、HashSet（线程不安全）、HashTable & SysnchronizedMap（线程安全）、ConcurrentHashMap（线程安全）
    * HashTable & SysnchronizedMap所有方法都同步synchronized了，但效率低
    * ConcurrentHashMap的分段锁称为Segment，ConcurrentHashMap采用了分段锁的设计，只有在同一个分段内才存在竞态关系，不同的分段锁之间没有锁竞争。
    * ConcurrentHashMap基于concurrencyLevel划分出多个Segment对key-value进行存储，避免每次put操作都得锁住整个数组。默认情况下，可允许16个线程并发无阻塞的操作集合对象。
* TreeSet：基于TreeMap（线程不安全）、TreeMap：基于红黑树-自平衡二叉查找树（线程不安全）
5. JVM垃圾回收机制
* 引用计数，若引用为0，则回收
6. Java类加载机制
* Class文件的生命周期：加载（Loading）、验证（Verification）、准备（Preparation）、解析（Resolution）、初始化（Initialization）、使用（Using）、卸载（Unloading）
7. 同步和互斥
* 互斥是某一资源仅允许一个访问者访问，排他性
* 同步是在互斥的基础上，通过其他机制实现访问者对资源的有序访问

## Deep Learning面试
1. Java内部类和外部类
* 内部类可以获取外部类的private属性，外部类可以访问内部类的private属性，真正执行是编译器的`acess$0`, `access$1`等
2. 设计模式
* 单例模式
    * 私有构造函数
    * 有static私有对象
    * 有static共有getInstance方法(创建或获取实例)
3. Servlet
* 继承HttpServlet，重写doGet()和doPost()方法
* 生命周期
    * 三个核心方法：init()，service()以及destroy()
    * Servlet生命周期的初始化阶段，web容器通过init()方法初始化Servlet实例
    * 初始化后，web容器调用Servlet的service()方法处理每一个请求
    * 最终，web容器调用destroy()方法终结Servlet
4. ArrayList和LinkedList的区别
* ArrayList是基于动态数组的数据结构，LinkedList是基于链表的数据结构
* ArrayList查找优于LinkedList，LinkedList新增和删除优于ArrayList
5. 数据库ACID
* Atomicity原子性
* Consistency一致性
* Isolation隔离性
* Durability持久性

## Deep Learning现场
1. a-z表示26进制
* 写代码，$26^0+26^1+...$
2. n个数找前k大
* 写代码
    * 法一：堆排序n*logn
    * 法二：先选择k个数，按序排列（k*logk），再二分查找比对，往里插，用n*logk（每一个二分查找是logk，一共n-k次）（避免查找后数组值的移动，将前k个数用链表表示）
    * 法三：最小/大堆法，将k个数建堆，依次将后来的数字插入，然后剩余的堆就是Top-K  
    * 更多思路见[10亿个数中找出最大的10000个数（top K问题）](http://blog.csdn.net/zyq522376829/article/details/47686867)

[返回目录](../CONTENTS.md)