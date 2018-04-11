# 大讲堂

1. HTTP缓存
* 强缓存： 直接从缓存中获取资源而不经过服务器
* 弱缓存（协商缓存）：
    * Last-Modified：文档最后修改时间，发送到服务端进行内容变更验证
    * Etag：标记，发送到服务端进行内容变更验证，若没有改变，返回304
    * Expires：不过期就使用缓存数据，不向服务器请求，适合于不经常变动的资源
2. 高可用：冗余、故障检测、fail over（失效转移）
3. Redis
* 高性能的key-value数据库，支持master-slave模式的数据备份
4. IO多路复用的事件分发器模式
* Reactor：同步IO，关键：IO多路复用
* Proactor：异步IO
5. CGI：Common Gateway Interface
* 一种协议，Web Server将动态请求和相关参数发送给专门的进程/线程
6. 操作缓存和DB
* write through写直达：数据更新，同时写入cache和DB
* write back写回：数据更新，只写入cache，当cache被替换时，被修改的数据写入DB
7. 消息队列
* 消息生产者Producer：发送消息到消息队列
* 消息消费者Consumer：从消息队列接收消息
8. 高延迟场景下提供足够的并发：
* group commit：组提交
* sliding window（TCP中的滑动窗口）：有顺序
* parallel pipeline：无顺序，多个RPC返回
9. REDO和UNDO
* REDO：先写log，commit之前不写磁盘，空闲时间写
* UNDO：先写磁盘，然后写UNDO log和CMT log
10. 页面替换算法
* 页面部分装入内存
* OPT（Optimal最佳替换算法）、FIFO、LFU（Least Frequently Used最不频繁使用）、LRU（Least Recently Used最近最少使用）

[返回目录](../CONTENTS.md)