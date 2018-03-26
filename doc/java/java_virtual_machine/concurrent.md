# Java高并发

## 乐观锁和悲观锁（实现线程安全）
### 定义
* 乐观锁：假设冲突不经常发生，先提交操作，如果失败就重试
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
        * 关键：1）volatile修饰state，判断是否有加锁；2）AQS同步器实现锁的获取与释放；
        * TryAcquire()方法：如果锁state为0则尝试获取锁，否则：识别获取锁的线程是否为当前占据锁的线程，如果是再次成功获取
* 信号量Semaphore
    * 信号量是对锁的扩展，sychronized和重入锁ReentrantLock一次只允许一个线程访问一个资源，信号量可以指定多个线程同时访问一个资源
    * 信号量可以用于做**流量控制**，控制最大并发量
    * 实现与ReentrantLock一样，依靠继承自AbstractQueuedSynchronizer的Sync实现主要功能，只是调用共享模式的：tryAcquireShared()方法

### 锁优化
* 适应性自旋（Adaptive Spinning）、锁消除
（Lock Elimination）、锁粗化（Lock Coarsening）、轻量级锁（Lightweight Locking）和偏向锁（Biased Locking）

### 读写锁
* 读写锁可以由悲观锁或乐观锁实现，一般：读不加锁，写加锁

## 线程池
### 定义
* 为避免系统频繁地创建和销毁线程，让创建的线程复用
![](./img/concurrent_1.png)
* Executors是一个静态工厂类，可以取得特定功能的线程池

### 不同特性的线程池（Executors中获取）
* newFixedThreadPool()
    * 返回固定数量的线程池
    * 当有新任务提交时，线程池中若有空闲线程，则立即执行，否则将任务放入任务队列
* newSingleThreadExecutor()
    * 返回只有一个线程的线程池
* newCachedThreadPool()
    * 返回一个可以根据实际情况调整线程数量的线程池，任务增多线程增加，任务减少线程减少
* newScheduledThreadPool()
    * 返回可指定线程数量的ScheduledExecutorService对象的定时线程池，可以：1）给定时间执行某任务（schedule()）；2）周期性执行某任务（scheduleAtFixedRate()）；3）固定延迟后，周期性执行某任务（scheduleWithFixedDelay()）。

### ThreadPoolExecutor线程池类
* 关键构造函数参数
    * corePoolSize：池中所保存的线程数，包括空闲线程
    * workQueue：被提交但尚未执行的任务队列
* 关键数据结构
    * HashSet<Worker> workers：一个worker对应一个线程，线程池通过workers包含多个线程
    * BlockingQueue<Runnable> workQueue：当线程池中的线程数超过容量，任务提交后，进入阻塞队列
    
## Future和FutureTask
* Future模式是多线程开发中常见的设计模式，核心思想是：异步调用
* Future是接口，FutureTask是具体实现类
* 客户端向服务器发送数据请求，服务器先返回代理数据，再启动新的线程加载真实数据，传递给代理对象
* 用法
```
Future<HashMap> future = getDataFromRemote();
//do something
HashMap data = future.get();
```

## 缓存
* 写流程：1）淘汰cache；2）再写db
* 读流程：1）读cache，如果数据命中hit则返回；2）如果数据未命中miss则读db；3）将db中读取出来的数据入缓存；

注：高并发访问数据库优化
1. 读写分离（master、slave数据库分别读写）
2. 分表分库存储
3. 缓存如Memcached，数据库修改后更新缓存
4. 将关系型数据库变为非关系型
5. 重要业务数据存储、不重要业务数据可临时存储
