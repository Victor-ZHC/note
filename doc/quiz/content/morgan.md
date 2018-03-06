# 摩根斯坦利
1. ArrayList
2. final
* 作用于类：该类不可以继承
* 作用于方法：继承后，该方法不可以覆盖
* 作用于变量：变量初始化后不可以改变
3. C++虚函数virtual关键字
* 实现了多态
* C++中，继承后重写方法，必须被声明为virtual
4. Java重写(override）和重载（overload）
* 重写：子类继承父类，重写方法
* 重载：一个类中，方法名相同，参数不同
5. 数据库索引
* 如：B+树索引，索引存在存储和处理开销，索引的创建和维护需要消耗时间和空间，数据的更新，索引也要动态维护
6. HashMap
* put(k,v)
* get(k)
7. 命令
* 打印当前系统正在运行的进程：ps
* 查看文件内容：ls –l
* 统计当前目录下文件的个数：ls -l | grep "^-" | wc -l
    * 解析：过滤ls的输出信息，仅保留文件
8. 队列和栈
* 队列：先进先出
* 栈：后进先出

## 终面1
1. Java内存分配
* 堆：存放new产生的数据；
* 栈：存放基本数据类型和对象的引用；
* 寄存器：程序无法控制；
* 静态域：存放static定义的静态成员；
* 常量池：存放常量；
2. JVM
* java虚拟机，使得java跨平台
3. java反射机制
* 动态获取类的所有属性和方法，调用对象的任意方法和属性
* 软件包：java.lang.reflect，提供类和接口，获取关于类和对象的反射信息
4. 并发与同步区别
* 并发有2种
    * 同步：后一个进程等待前一个进程的输出
    * 互斥：相互排斥使用临界资源
5. 进程与线程的区别
* 进程：资源分配与保护的基本单位allocate and protect system resources；
* 线程：系统调度和分派的基本单位；schedule and dispatch system；
* 一个线程只能属于一个进程，但一个进程可以拥有多个线程；
* 进程是拥有资源的基本单位，线程不拥有资源，但可以访问进程的资源；
6. finalize什么时候调用
* System.gc( )时；
* 程序退出时；
7. 什么时候用finally
* 例如：文件或数据库的close
* 如果try或catch有return指令，finally仍然会执行，流程跳到finally，然后回调return；


## 终面2
1. Object子类的方法举例
* String: charAt、compareTo、concat、endsWith、indexOf、length、replace、split、subString、toCharArray、trim
* StringBuffer: append
* Integer: intValue、parseInt
* Date: getTime、setTime、toString
* Math: min、max、abs、random、sin、pow
2. Object类的方法
* toString、equals、notify、notifyAll、clone、hashCode、getClass、finalize、wait
3. meta charset
* `<meta charset=“UTF-8”>`
4. Web页面相对位置不会移动
* 采用百分比而不是绝对的像素值
5. 记录出现不止一次的邮箱
```
ArrayList<String> emailList = new ArrayList<String>();   // 所有邮箱
HashSet<String> uniqueSet = new HashSet(emailList);   // 不重复记录
ArrayList<String> oneMoreEList = new ArrayList<String>();   // 所有不止一次出现的邮箱
for(String temp : uniqueSet)
    if(Collections.frequency(emailList, temp)>0)  // 出现不止一次的邮箱
        oneMoreEList.add(temp);
for(String temp : oneMoreEList){
    String s = "";
    // 比对用户邮箱，输出用户名
}
```

[返回目录](../CONTENTS.md)