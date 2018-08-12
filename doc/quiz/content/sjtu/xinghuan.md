# 星环科技
1. Spark相关，参考[Spark](../../learn/distribution.md)
2. 小于等于k的最大连续子序列和
```
public int maxSumNoLargerThan1(int[] array, int k){  
    int r = Integer.MIN_VALUE;  
    for(int i = 0; i < array.length; i++){  
        int sum = 0;  
        for(int j = i; j < array.length; j++){  
            sum += array[j];  
            if(sum <= k)  
                r = Math.max(r, sum);  
        }  
    }  
    return r;  
}
```
3. 二叉树中最远两个节点的距离，递归求解
* http://blog.csdn.net/qq_33417547/article/details/53423230
* 有两种情况
    * 情况1：路径经过左子树的最深节点，通过根节点，再到右子树的最深节点；
    * 情况2：路径不穿过根节点，而是左子树或右子树的最大距离路径，取其大者；
* 最终：取两种情况的最大值

[返回目录](../../CONTENTS.md)