# 排序
## 插入排序
* 思想：n个对象已排好序，插入第n+1个对象到适当位置
* 方法：直接插入排序、折半插入排序、链表插入排序、希尔排序

1. 直接插入排序
```
public static void insertionSort( Comparable [] a ) {
      int j;
      for ( int p = 1; p < a.length; p++ ) {
           Comparable tmp = a[p];
           for ( j = p; j > 0 && tmp.compareTo(a[j – 1])<0; j-- )
                 a[j] = a[j – 1];
            a[j] = tmp;
       }
}
```
* 稳定性：稳定
* O（N^2）

2. 折半插入排序（二分法插入排序）
```
template <class Type> void  BinaryInsertSort( datalist<Type> &list) {
    for (int i=1; i<list.currentSize; i++)
         BinaryInsert(list, i);
}                                         
template <class Type> void  BinaryInsert( datalist<Type> &list,  int i) {
      int left=0,  Right=i-1;
      Element<Type>temp=list.Vector[i];
      while (left<=Right) {
         int middle=(left+Right)/2;
         if (temp.getkey()<list.Vector[middle].getkey())
             Right=middle-1;
         else left=middle+1;
      }
      for (int k=i-1; k>=left; k--)
         list.Vector[k+1]=list.Vector[k];
      list.Vector[left]=temp;
}
```