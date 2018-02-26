# 算法分析
## Space Complexity 空间复杂度（两部分）
* fixed part：指令、简单变量、固定大小的成员变量、常量
* variable part：成员变量、动态分配空间、递归栈

## Time Complexity 时间复杂度（两部分）
* Compile Time 编译时间
* Run Time 运行时间

## Sort
* Bubble Sort 冒泡排序 
    * $O(n^2)$，每次扫描将最大元素冒泡到最后
```
public int[] sort(int[] a) {
    int temp;
    for (int i = a.length - 1; i > 0; i--) {
        for (int j = 0; j < i; j++) {
            if (a[j + 1] < a[j]) {
                temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }
    return a;
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
        
## 复杂度分析
* O：upper bound for function f 上限
* Ω：lower bound for function f 下限
* θ：when the function f can be bounded both from above and below by the same function g
* o：表示f(x)趋近于g(x)

## Binary Search 二分查找/折半搜索
```
public static int binarySearch( Comparable[] a, Comparable x ) {
    int low = 0, high = a.length - 1;
    while( low <= high ) {
        int mid = ( low + high ) / 2;
        if(  a[mid].compareTo(x) < 0 )
            low = mid + 1;
        else if( a[mid].compareTo(x) > 0 )
            high = mid – 1;
        else
            return mid;
   }
   return NOT-FOUND;
}
```

## Euclid's Algorithm（辗转相除法）
* 求最大公因子 O(logN)
```
public static long gcd( long m, long n ) {   
    while( n != 0 ) {    
        long rem = m % n;
        m = n;
        n = rem;
    }
    return m;
}
```

[返回目录](../CONTENTS.md)