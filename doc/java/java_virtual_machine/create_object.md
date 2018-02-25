# 对象创建
1. 当遇到一条new指令时，首先检查指令的参数能否在常量池中定位到一个类的符号引用
2. 对象的大小在类加载完成后便可完全确定，之后从Java堆中将内存划分出来即可
    * 如果Java堆中的内存是规整的（占用的内存和空闲内存分离），中间使用指针作为分界线，分配内存即将指针挪动对象大小的距离，称为指针碰撞（Bump the Pointer）
    * 如果Java堆中的内存不是规整的，则需要一个列表来记录哪些内存块是可用的，分配内存时通过列表去查找可用的内存，这种分配方式被称为空闲列表（Free List）
    * 不同方式取决与GC是否带有压缩整理的功能
3. 在并发的情况下，内存分配可能出现错误，解决方案有两种
    * 分配内存的动作进行同步处理
    * 把内存分配的动作按照线程划分在不同的空间之中进行，每个线程预先在Java堆中分配一小块内存，成为本地线程分配缓冲（Thread Local Allocation Buffer，TLAB），当TLAB用完需要分配新的TLAB时，才需要同步锁定
4. 将内存空间初始化为0值
5. 对对象头进行设置（哪个类的实例、哈希码，GC分代年龄等信息）
6. 执行<init>方法，对对象进行初始化

[返回目录](../CONTENTS.md)