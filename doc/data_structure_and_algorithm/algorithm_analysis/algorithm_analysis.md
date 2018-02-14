# 算法分析
## Space Complexity 空间复杂度（两部分）
* fixed part：指令、简单变量、固定大小的成员变量、常量
* variable part：成员变量、动态分配空间、递归栈

## Time Complexity 时间复杂度（两部分）
* Compile Time 编译时间
* Run Time 运行时间

## Sort
* Bubble Sort 冒泡排序 
    * O((n-1)*n/2)=O(n^2)，每次扫描将最大元素冒泡到最后
```
public static void Bubble(int[] a , int n) {
    //Bubble largest element in a[0:n-1] to right
    for(int i=0; i<n-1; i++)
        if(a[i]>a[i+1])
            swap(a[i],a[i+1]);
}
public static void BubbleSort(int[] a, int n) {
    //Sort a[0:n-1] using a bubble sort
    for(int i=n ;i>1; i--)
        Bubble(a,i);
}
```

* Selection Sort 选择排序
    * O((n-1)*n/2)=O(n^2)，找最大
```
public static void SelectionSort( int[] a, int n) {
    //sort the n number in a[0:n-1].
    for(int size=n; size>1; size--) {
        int j=Max(a,size);
        swap(a[j],a[size-1]);
    }
}
```

* Rank Sort 计数排序
    * O((n-1)*n/2)=O(n^2)，计数值，比该元素小的数值个数
```
public static void Rank( int[] a, int n, int[] r) {
    //Rank the n elements a[0:n-1]
    for(int i=0;i<n;i++)
        r[i]=0;
    for(int i=1;i<n;i++)
        for(int j=0;j<i;j++)
            if(a[j]<=a[i]) 
                r[i]++;
            else r[j]++;
}
public static void Rearrange( int[] a, int n, int[] r) {
    //In-place rearrangement into sorted order
    for(int i=0;i<n;i++)
        while(r[i]!=i) {
            int t=r[i];
            swap(a[i],a[t]);
            swap(r[i],r[t]);
        }
}
```

* Insertion Sort 插入排序
    * O((n-1)*n/2)=O(n^2)，第一个元素默认，从第二个元素开始从后往前比较插入
```
public static void Insert( int[] a , int n, int x) {
    //Insert x into the sorted array a[0:n-1]
    int i;
    for(i=n-1; i>=0 && x<a[i]; i--)
        a[i+1]=a[i];
    a[i+1]=x;
}
public static void InsertionSort( int[] a, int n) {
    for(int i=0; i<n; i++) {
        int t = a[i];
        Insert(a,i,t);
    }
}
```

* Radix Sort 桶排序
    * 时间复杂度小，空间复杂度大，过多地占用内存
        * 个位数比较，放入相应桶内
        * 清空桶，比较十位
        * 清空桶，比较百位
        * 回收结果