# 拼多多
1. 程序导致CPU占用率100%，排查方法
* top命令查看启动的进程的CPU占用率，找出100%的进程
2. 程序不断GC
* 因为：资源泄漏
3. Comparator
```
public class Compare implements Comparator<Activity> {
    @Override
    public int compare(Activity a1, Activity a2) {}
}
调用：
Collections.sort(activityList, new Compare());
```
4. Comparable
```
public class Activity implements Comparable<Activity> {
    @Override
    public int compareTo(Activity a) {}
}
调用：
Collections.sort(activityList);
```

[返回目录](../../CONTENTS.md)