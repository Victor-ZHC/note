# 京东
1. ArrayList和LinkedList都实现了List接口
2. @Transactional，Spring-boot中的事务
3. Java堆通过Xmx和Xms指定最大内存和最小内存
4. Linux的sed：是一种流编辑器
5. **java.lang.ThreadLocal**
* ThreadLocal为每个使用该变量的线程提供独立的变量副本，每个线程独立地改变自己的副本，而不影响其他线程的副本
* 通常ThreadLocal实例使用private static修饰，将状态与线程相关联
* ThreadLocal中有一个内部类ThreadLocalMap，存值：<ThreadLocal对象，存放的值>，优点：每一个线程对应一个ThreadLocalMap，一个线程可以有多个线程本地变量

* 不是用来解决共享变量或者线程同步的
* [参考链接](http://www.cnblogs.com/zhengbin/p/5674638.html)
* 使用
![](../img/threadlocal.png)

[返回目录](../../CONTENTS.md)