# 爱奇艺
1. 矩阵相乘
```
double[][] c=new double[a.length][b[0].length];
for(int i=0;i<a.length;i++) {
      for(int j=0;j<b[0].length;j++) {
           for(int k=0;k<a[0].length;k++) {            
               c[i][j] += a[i][k] * b[k][j]; 
            }
      }
}
```

[返回目录](../../CONTENTS.md)