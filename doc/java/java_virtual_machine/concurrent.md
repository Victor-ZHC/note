# Java高并发

## 乐观锁和悲观锁（实现线程安全）
### 定义
* 乐观锁：假设冲突不经常发生，先提交操作，如果失败就重试
* 悲观锁：假设会发生冲突，有强烈的独占和排他性

### 乐观锁应用
* 非阻塞同步，乐观的并发策略
1. CAS操作
* 比较并交换，Compare-and-Swap，可以通过一条处理器指令完成
* java.util.concurrent.atomic包下的原子类型变量，如：AtomicInteger，使用了底层的JVM支持，为数字类型提供CAS操作
* CAS操作会出现ABA问题，解决：不只更新引用值，而是更新引用+版本号，即使出现ABA，版本号也不
同

### 悲观锁应用
* 互斥同步（Mutual Exclusion & Synchronization），悲观的并发策略
1. 互斥是同步的手段，临界区（Critical
Section）、互斥量（Mutex）和信号量（Semaphore）都是主要的互斥实现方式
2. Java中互斥
* synchronized关键字
    * 编译后在同步块前后产生monitorenter和monitorexit指令
* 重入锁（ReentrantLock）
http://www.cnblogs.com/zhengbin/p/6503412.html
    * java.util.concurrent包中
    * 与synchronized类似
        * synchronized是原语层面的互斥锁，而ReentrantLock是API层面的互斥锁
        * 都可以线程重入（是同一个线程可以反复使用其占用的锁，相当于一个偏向锁）
        * 但ReentrantLock增加的3个功能
            1. 等待可中断：持有锁的线程长期不释放锁，等待锁的线程可放弃等待
            2. 可实现公平锁：公平锁指：多个线程等待同一个锁时，必须按照申请的顺序依次获得锁（默认是：非公平锁）
            3. 锁绑定多个条件：一个ReentrantLock对象可以同时绑定多个Condition对象（多次调用newCondition()方法），而synchronized只能一个
* 信号量

### 锁优化
* 适应性自旋（Adaptive Spinning）、锁消除
（Lock Elimination）、锁粗化（Lock Coarsening）、轻量级锁（Lightweight Locking）和偏向锁（Biased Locking）

### 读写锁
* 读写锁可以由悲观锁或乐观锁实现，一般：读不加锁，写加锁

## 线程池


## 缓存
* 写流程：1）淘汰cache；2）再写db
* 读流程：1）读cache，如果数据命中hit则返回；2）如果数据未命中miss则读db；3）将db中读取出来的数据入缓存；

## 分布式情况下负载均衡
