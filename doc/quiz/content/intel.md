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
4. 线程安全
* ArrayList（线程不安全）和Vector（线程安全）
    * Vector所有方法都同步synchronized了
        * synchronized实现：monitorenter和monitorexit
* HashMap（线程不安全）、HashTable（线程安全）、ConcurrentHashMap（线程安全）
    * HashTable所有方法都同步synchronized了，但效率低
    * ConcurrentHashMap每一个Segment都拥有一个锁
5. JVM垃圾回收机制
* 引用计数，若引用为0，则回收
6. Java类加载机制
* Class文件的生命周期：加载（Loading）、验证（Verification）、准备（Preparation）、解析（Resolution）、初始化（Initialization）、使用（Using）、卸载（Unloading）

## Deep Learning面试
1. Java内部类和外部类
* 内部类可以获取外部类的private属性，外部类可以访问内部类的private属性，真正执行是编译器的acess$0, access$1等
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