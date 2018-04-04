# 线程池
## 定义
* 为避免系统频繁地创建和销毁线程，让创建的线程复用
![](./img/thread_pool_1.png)
* Executors是一个静态工厂类，可以取得特定功能的线程池

## 不同特性的线程池（Executors中获取）
* newFixedThreadPool()
    * 返回固定数量的线程池
    * 当有新任务提交时，线程池中若有空闲线程，则立即执行，否则将任务放入任务队列
* newSingleThreadExecutor()
    * 返回只有一个线程的线程池
* newCachedThreadPool()
    * 返回一个可以根据实际情况调整线程数量的线程池，任务增多线程增加，任务减少线程减少
* newScheduledThreadPool()
    * 返回可指定线程数量的ScheduledExecutorService对象的定时线程池，可以：1）给定时间执行某任务（schedule()）；2）周期性执行某任务（scheduleAtFixedRate()）；3）固定延迟后，周期性执行某任务（scheduleWithFixedDelay()）。

## ThreadPoolExecutor线程池类
* 关键构造函数参数
    * corePoolSize：池中所保存的线程数，包括空闲线程
    * workQueue：被提交但尚未执行的任务队列
* 关键数据结构
    * `HashSet<Worker> workers`：一个worker对应一个线程，线程池通过workers包含多个线程
    * `BlockingQueue<Runnable> workQueue`：当线程池中的线程数超过容量，任务提交后，进入阻塞队列

[返回目录](../CONTENTS.md)