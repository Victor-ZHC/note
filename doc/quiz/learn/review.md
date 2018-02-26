# Review
## 关于GC
1. 内存废弃对象检测算法：引用计数器算法和可达性分析算法。可达性分析算法：即：当GC Roots到某个对象不可达时，判断该对象是废弃的。现一般都用可达性分析算法，因为引用计数算法存在循环引用的问题。
2. 强引用，软引用，弱引用，虚引用
* https://www.cnblogs.com/yw-ah/p/5830458.html
* 强：Object obj = new Object();
* 软：SoftReference，内存不足时自动删除
* 弱：WeakReference，isEnQueued()判断是否被垃圾回收器标记
* 虚：PhantomReference，isEnQueued()判断是否已经从内存中删除
3. 垃圾回收算法
* 标记清除算法：标记所有需要清除的对象，之后统一清除
* 复制算法：将内存分为一块Eden和两块Survivor，一般比例：8:1，每次将Eden和一个Survivor上存活的对象复制到另一个Survivor上
* 标记整理算法：标记所有存活的对象，并移到内存一端
* 分代收集算法：将内存分为新生代和老生代

## 关于类加载
* 类加载机制：加载、验证、准备、解析、初始化、使用、卸载

## java
* Volatile：java提供的稍弱的同步机制，即：volatile变量，确保将变量的更新操作通知到其他线程

## 线程状态
* 新建（new）、可运行（runnable）、运行（running）、阻塞（blocked）、死亡（dead）

## 异常级别
* Exception(IOException, InterruptedException, RuntimeException(ClassCastException, NullPointerException))
* ClassCastException类型转化出错

## Math类
* Math构造函数是私有的，不可以实例化，并且是final类，不可以被继承
* 因此：不可以被实例化 1）抽象类 2）私有构造函数


[返回目录](../CONTENTS.md)