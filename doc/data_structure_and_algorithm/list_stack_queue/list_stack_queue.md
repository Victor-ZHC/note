# 列表，栈和队列
## 列表
* 数组实现表：返回给定元素方便，但插入、删除复杂（∵存在数组移动），如：ArrayList
* 链表实现表：有数据域存放数据、链接域指向下一元素，如：LinkedList

## LinkedList
* ListNode 代表结点的类
```
class ListNode {
    ListNode( object theElement) {
        this( theElement, null);
    }
    ListNode( object theElement, ListNode n) {
        element = theElement;
        next = n;
    }
    object element;
    ListNode next;
}
```

## 栈
* LIFO（last-in-first-out）
* 链表实现或者数组实现

## 队列
* FIFO（first-in-first-out）
* 链表实现或者数组实现

[返回目录](../CONTENTS.md)