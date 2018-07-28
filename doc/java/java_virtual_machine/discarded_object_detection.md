#内存废弃对象检测

## 引用计数器算法
为对象添加一个引用计数器，每当有一个地方引用它时，计数器就加1；引用失效时，计数器减1；当计数器为0时，对象就是不可被引用的
* 优点是简单，判定效率高
* 缺点是难以解决对象之间循环引用的问题

## 可达性分析算法
通过一系列称为GC Roots的对象作为起点，当GC Roots到某个对象不可达时，判定此对象是废弃的，从GC Roots到对象所经过的路径被称为引用链（Reference Chain）

可以作为GC Roots的对象包括：
* 虚拟机栈中引用的对象
* 方法区中类静态属性引用的对象
* 方法区中常量引用的对象
* 本地方法栈中Native方法引用的对象

## 引用
### 强引用（Strong Reference）
普遍存在，就是类似Object obj = new Object()的引用，只要强引用还在，垃圾回收器就不会回收被引用的对象

### 软引用（Soft Reference）
描述之前还有但并非必须的对象，在系统将要发生内存溢出异常之前，将会把这些对象列入回收范围之中进行第二次回收

### 弱引用（Weak Reference）
被弱引用关联的对象只能生存到下一次垃圾收集发生之前

### 虚引用（Phantom Reference）
对象是否有虚引用与其生存时间无任何关系，设置虚引用的目的仅是在对象被系统回收时收到一个系统通知

## 对象死亡
当对象不可达时，垃圾回收器还需要判定对象是否有必要执行finalize()方法 ，当判定对象有必要执行finalize()方法时，那么对象将暂时放在一个F-Queue队列之中，并在一个低优先级线程中执行finalize()，但finalize()方法不一定能够运行结束

```
public class EscapeGC {
    public static EscapeGC SAVE_HOOK = null;

    public void isAlive() {
        System.out.println("i am still alive");
    }

    @Override
    protected void finalize() throws Throwable {
        super.finalize();
        System.out.println("finalize method executed!");
        EscapeGC.SAVE_HOOK = this;
    }
}

public class EscapeGCTest {
    @Test
    public void testEscapeGC() throws Exception {
        EscapeGC.SAVE_HOOK = new EscapeGC();

        EscapeGC.SAVE_HOOK = null;
        System.gc();
        Thread.sleep(500);
        if (EscapeGC.SAVE_HOOK != null) {
            EscapeGC.SAVE_HOOK.isAlive();
        } else {
            System.out.println("i am dead");
        }

        EscapeGC.SAVE_HOOK = null;
        System.gc();
        Thread.sleep(500);
        if (EscapeGC.SAVE_HOOK != null) {
            EscapeGC.SAVE_HOOK.isAlive();
        } else {
            System.out.println("i am dead");
        }
    }
}
```

> 结果：  
finalize method executed!  
i am still alive  
i am dead  

[返回目录](../CONTENTS.md)