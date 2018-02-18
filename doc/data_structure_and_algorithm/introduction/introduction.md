# Introduction
## ADT
* Abstract Data Type
* 将类型和与类型有关的操作集合封装在一起的数据模型，目的：encapsulate and hide information

## 算法特性
* 有穷的、确定的、有初始步骤、顺序结束

## 证明方法
* Induction 归纳法
    * base case
    * inductive hypothesis 归纳假设
* Contradiction 矛盾法

## 递归
* Base cases + Making progress
* Factorial 阶乘 f(n)=n!
```
static long factorial (int n)  {   
    if ( n <= 1)
        return  1;
    else return n* factorial( n-1 )
}
```
* Fibonacci 斐波拉切数列
```
public static long fib(long n) {
    if ( ( n = = 0) || ( n = = 1 ) )
        return n;
    else
        return  fib(n-1) + fib(n-2);
}
```
* Permutation 排列
```
public static void perm(Char[] list ,  int k,  int m) {   
    int i;
    if (k==m) { 
        for (i=0; i<=m; i++) 
            cout << list[i];
        cout << endl; 
    }
    else{ 
        for (i=k; i<=m; i++) { 
            swap(list[k], list[i]);
            perm(list, k+1, m);
            swap(list[k], list[i]);
        }
    }
} 
```
* Combination 组合
```
public static void combine(int n,int[] list,int r) {
    for (int i=n; i>0; i--) {
        list[r-1] = i;
        if (r>1) {
            combine(i-1, list, r-1);
        } else {
            for (int j : list)
                System.out.print(j);
            System.out.println();
        }
    }
}
```

## java基础
* 所有objects都是Object类的子类
    * primitive types: boolean, short, char, byte, int, long, float, double不是objects
    * wrapper class包装类，提供方法可以访问primitive value，如Integer中的intValue方法
```
public class Integer { 
    private int value; 
    public Integer(int x) {
        value = x; 
    }
    public int intValue( ) {
        return value; 
    }
}
```

* FindMax
```
public static Comparable findMax(Comparable[] arr)  {
    int maxIndex = 0;
    for ( int i = 1; i < arr.length; i++ )
            if ( arr[i].compareTo(arr[maxIndex]) > 0 )
                maxIndex = i ;
    return arr[maxIndex];
}
```

## 三类errors
* 语法error：编译时发现，又称编译错
* 语义error：运行时发现，又称运行错，包括：
    * 错误error：硬件或OS错误
    * 异常exception：程序运行错误
* 逻辑error：结果与期望值不符

## Input
* System.in->InputStreamReader->BufferedReader
* fileName->FileReader->BufferedReader
```
BufferedReader in = new BufferedReader( new InputStreamReader ( System.in ) );
// 或者 BufferedReader in = new BufferedReader( new FileReader ( fileName ) );
int x;
String oneLine;
try {
    oneLine = in.readLine( );   //  IOException
    x = Integer.parseInt( oneLine );  //NumberFormatException
    System.out.println( “x is “ + x );
} catch( Exception e ) {
    system.out.println( e ); 
}
```

[返回目录](../CONTENTS.md)