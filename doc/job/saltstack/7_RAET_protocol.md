# 理解RAET协议
* RAET：Reliable Asynchronous Event Transport，可靠异步事件传输

## 比对RAET与ZeroMQ
* HTTP的限制，请求和响应必须是一个文档（document）
* ZeroMQ从未被设计用于配置管理，其设计目标是：一个快速、简单的高级消息队列协议（Advanced Message QUeuing Protocol，AMQP）的替代品，和AMQP是一个作者设计的
* ZeroMQ起初并未实现任何形式的安全性，没有加密开销；而Salt设计运行在并非所有用户都可信的网络中，所有消息都加密
* ZeroMQ基于以可靠性著称的TCP协议；而RAET基于以非可靠性著称的UDP协议

## 使用RAET
### 配置RAET
* 在Master和Minion的配置文件中设置transport为raet

### RAET架构
* Salt使用客户端/服务器端模式
* RAET总线上的主机叫estate，每个estate至少有一个yard，estate之间互连可以通过road或lane；lane用于连接同一台物理主机上的estate，road用于连接不同物理主机上的estate

### RAET调度器
* 与ZeroMQ一样，RAET也基于队列，在RAET中称为堆栈（stack）


[返回目录](../CONTENTS.md)