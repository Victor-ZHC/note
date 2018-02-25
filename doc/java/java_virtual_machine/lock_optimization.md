# 锁优化
## 自旋锁与自适应自旋
* 互斥部分的代码执行时间一般很短
* 不再让冲突的线程等待（阻塞恢复的代价是很大的），而是让线程进入一个忙循环（自旋）
* 如果自旋超过一定次数，就让冲突的线程阻塞
* 自适应自旋就是根据前一次在相同锁上的自旋时间来决定本次自旋的时间

## 锁消除
* 即时编译器在运行时，对代码上要求同步，但是被检测到不可能存在共享数据竞争的锁进行消除

## 锁粗化
* 当一系列连续的操作都对一个对象进行反复的加锁和解锁，甚至加锁操作是放在循环体中的，会出现大量的性能损耗，锁粗化就是将这些操作合并在一个同步块中

## 轻量级锁
* 利用对象的头信息中的“Mark Word”部分，使用CAS操作尝试将其更新为指向Lock Record的指针（包含owner和Displaced Mark Word（用于存放原Mark Word的））。
* 如成功说明已经拥有锁，标志位转为“00”
* 如果失败，首先检查“Mark Word”是否指向当前栈帧，如果是，直接进入同步块，否则说明锁对象已经被其他线程抢占，膨胀为重量级锁，标志位变成“10”
* 解锁过程使用CAS将Displaced Mark Word替换到Mark Word部分，如果替换成功，同步完成，替换失败，说明有其他线程尝试获取该锁，在释放的同时，唤醒被挂起的线程
* 提升性能是依据绝大部分锁是不存在竞争这一前提下的

## 偏向锁
* 基于轻量级锁的进一步优化，
* 锁第一次被线程获取的时候，用CAS把获取锁的线程ID记录在Mark Word中，如果CAS成功，则持有偏向锁，每次线程进入锁的同步块时，都不需要进行同步操作
* 当另一个线程获取该锁时，偏向模式就结束了，根据现在对象是否被锁定恢复到未锁定“01”或者轻量级锁定“00”，后续的同步操作依照轻量级锁执行

![](./img/lock_optimization_1.png)

[返回目录](../CONTENTS.md)