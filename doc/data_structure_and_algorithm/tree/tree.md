# 树
## 两种数据结构
* 线性结构：链表、栈、队列、string
* 非线性结构：树、图

## 二叉树的特点
* n个节点，n-1条边
* 第i层最多有2^i个节点
* 高为h的树，节点数最少h+1，最多2^(h-1)
* 叶子节点数为n0，度为2的节点数为n2，则：n0=n2+1
    * 证明：
    * 设度为1的节点数是n1，则：n=n0+n1+n2
    * n=B+1，B为分支数
    * 则：n0+n1+n2=1\*n1+2\*n2+1
    * 则：n0=n2+1
* n个元素的节点个数，最多：n-1，最少 「log2(n+1)」-1（上限）
```
class BianryNode {
      BinaryNode() {Left=Right=0;}
      BinaryNode(Object e) {element=e; Left=Right=0;}
      BinaryNode(Object e,  BinaryNode l, BinaryNode r) {element=e;  Left=l;  Right=r; }
      
       Object element;
       BinaryNode  left;    //left subtree
       binaryNode  right;   //right subtree
}

template<class T>class BinaryTree {
public:
         BinaryTree(){root=0;};
         ~BinaryTree(){};
         bool IsEmpty()const
             {return ((root)?false:true);}
         bool Root(T& x)const;
         void MakeTree(const T& data, BinaryTree<T>& leftch, BinaryTree<T>& rightch);
         void BreakTree(T& data , BinaryTree<T>& leftch, BinaryTree<T>& rightch);
         void PreOrder(void(*visit)(BinaryNode<T>*u)) {PreOrder(visit, root);}
         void InOrder(void(*visit)(BinaryNode<T>*u)) {InOrder(visit, root);}
         void PostOrder (void(*visit)(BinaryNode<T>*u)) {PostOrder(visit, root);}
         void LevelOrder (void(*visit)(BinaryNode<T> *u));
private:
         BinaryNode<T>* root;
         void PreOrder(void(*visit)(BinaryNode<T> *u), BinaryNode<T>*t);
         void InOrder(void(*visit)(BinaryNode<T> *u), BinaryNode<T>*t);
         void PostOrder(void(*visit) (BinaryNode<T> *u), BinaryNode<T>*t);
};
```

* PreOrder Traversal 前序遍历
```
template<class T>
void PreOrder(BinaryNode<T>* t) {
     // preorder traversal of *t.
     if(t) {
         visit(t);
         PreOrder(t->Left);
         PreOrder(t->Right);
     }
}
```

* InOrder Traversal 中序遍历
```
template<class T>
void InOrder(BinaryNode<T>* t) {
    if(t) {
        InOrder(t->Left);
        visit(t);
        InOrder(t->Right);
    }
}
```

* PostOrder Traversal 后序遍历
```
template<class T>
void PostOrder(BinaryNode<T>* t) {
    if(t){
           PostOrder(t->Left);
           PostOrder(t->Right);
           visit(t);
    }
}
```

## Binary Search Trees
```
private BinaryNode insert( Comparable x, BinaryNode t ) {
    if( t == null )
        t = new BinaryNode( x, null, null );
    else if( x.compareTo( t.element ) < 0 )
        t.left = insert( x, t.left );
    else if( x.compareTo( t.element ) > 0 )
        t.right = insert( x, t.right );
    else
        ;   //duplicate; do nothing
    return t;
}
```

## AVL 平衡的二叉搜索树
* 是二叉搜索树
* 满足|hL-hR|<=1，hL为左子树高度，hR为右子树高度
* 插入
    * 单旋
    * 双旋
    
## B tree 平衡的m叉搜索树
* 是扩充树
* 每个节点可包含多个（1->m-1个）键值
* 性质
    * 根节点至少2个子女
    * 除根节点外，其他所有内部节点，至少「m/2」（上限）个子女，最多m个子女
    * 所有外部节点都在同一层
    * 外部节点个数=键值总数+1
* 数据库索引结构，一般为B树或者B+树

## B+ tree
* 是B tree的一种变形，前4点同B tree，后2点不同
    1. 树中每个非叶节点最多有m棵子树
    2. 根节点（非叶节点）至少有2棵子树
    3. 除根节点外，每个非叶节点至少「m/2」（上限）棵子树
    4. 所有叶节点都处于同一层次
    5. 每个叶节点中，子树棵数n可以>m，也可以<m
    6. 根节点本身又是叶节点，则节点格式同叶节点
* 特点：关键码只分布在叶节点上

[返回目录](../CONTENTS.md)