# Disjoint Set
* 不相交集，即：等价类
* 当且仅当：Reflexive, Symmetric, Transitive满足
* Find & Union 代码
```
public class DisjSets {
    public DisjSets( int numElements )
    public void union( int root1, int root2 )
    public int find( int x )
    private int [ ] s;
}
public DisjSets( int numElements ) {
    s = new int [ numElements ];
    for( int i = 0; i < s.length; i++ )
        s[i] = -1; //一个根结点
}
public void union( int root1, int root2 ) {
    s[root2] = root1;
}
public int find( int x ) {
    if( s[x] < 0 )
        return x;
    else
        return find( s[x] );
}
```

[返回目录](../CONTENTS.md)