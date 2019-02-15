# 异步管理任务
* Salt的事件系统组成了基本的异步执行框架

## 事件系统
* Salt基于消息队列构建：命令由Master产生任务并推送到队列中，Minion监听队列中能够匹配到自己的任务；当Minion获取到一个任务时，会尝试执行；一旦任务完成，将执行结果发送到另一个Master监听的队列。
* Minion的消息块有两种基本的事件总线：1）Minion内部沟通的总线；2）Minion和Master沟通的总线；

### 事件数据结构
* 消息允许关联为事件数据（event data）或有效装载（payload），有效装载包含：时间戳（_stamp）、动作（action）、需要认证的Minion ID（id）以及Minion的公钥（pub）

### 查看事件数据
* 使用事件监听器：  
1. 事件监听器在Salt Master上运行，监听默认的socket路径
```
进入脚本的目录，执行：
# python eventlisten.py
```
2. 默认情况下，事件监听器使用Salt默认的传输机制：ZeroMQ

### 通用事件
```
1. salt/auth：Minion会使用该事件定期完成与Master的重认证
2. salt/key：当一个Minion的密钥被Master接受（accept）或拒绝（reject），将会发送该事件
3. salt/minion/<minion_id>/start：进程启动完毕，可以处理任务时，发送该事件
4. salt/job/<job_id>/new：创建新任务时，发送该事件
5. salt/job/<job_id>/ret/\<minion_id\>：一旦Minion完成任务，会发送一个包含返回数据的事件
6. salt/presence/present：只有当Master配置文件中presence_events设置为True时才会有该事件。当设置为True时，定期发送包含当前连接到Master上的Minion列表的事件
7. salt/presence/change：只有当Master配置文件中presence_events设置为True时才会有该事件。当设置为True时，有新的Minion连接到Master或从Master上断开连接，会发送该事件
```

### 通用云事件
* 当创建（create）或销毁（destroy）机器时，Salt Cloud会发送一些事件
```
1. salt/cloud/<vm_name>/creating：虚拟机创建
2. salt/cloud/<vm_name>/requesting：当所有用于创建虚拟机需要的信息收集后，Salt Cloud会从云供应商处产生一个虚拟机创建完毕的请求
3. salt/cloud/<vm_name>/querying：云供应商开始处理创建一个虚拟机并返回Salt Cloud能够用于指向的ID
4. salt/cloud/<vm_name>/waiting_for_ssh：当返回一个虚拟机IP地址时，并不代表虚拟机可用。Salt Cloud会等待虚拟机变成可用状态并且可以响应SSH连接
5. salt/cloud/<vm_name>/deploying：部署脚本
6. salt/cloud/<vm_name>/created：虚拟机已经成功创建
7. salt/cloud/<vm_name>/destroying：Salt Cloud可以产生一个请求给云供应商来销毁一个虚拟机
8. salt/cloud/<vm_name>/destroyed：Salt Cloud已经销毁该虚拟机
```

### Salt API事件
* Salt API是Salt内置的守护进程
```
1. salt/netapi/<url_path>：真实的URL路径依赖于Salt API的配置
```

## 构建反应器
* 反应器系统为用户提供一个构建异步和自助式的系统

### 配置反应器
* 反应器（Reactor）是Master端的进程，不需要直接在Minion上做任何配置

### 编写反应器
* 反应器系统支持3种不同种类的方法，分别是：执行模块、runner模块及管理Master的wheel模块
* 执行模块：运行在Minion端，需要在salt命令中指出有哪些Minion作为目标（target）需要执行
* runner模块：运行在Master端，不需要指定运行目标（target）
* wheel模块：用于管理Master自身，也不需要指定运行目标（target）

### 编写更复杂的反应器
* 发送告警，Salt中内置了一些模块用于发送告警，如：smtp和http执行模块

## 使用队列系统
* 使用默认的sqlite队列模块，若想获得在sqlite中存放的队列列表，使用命令：
```
# salt-run queue.list_queues backend=sqlite
```
* 队列系统通过runner进行管理，即：队列数据库只能被Master访问

### 添加项目到队列
```
# salt-run queue.insert myqueue item1
True
# salt-run queue.insert myqueue '["item2", "item3"]'
True
```

### 列出队列
```
# salt-run queue.list_queue
- myqueue
```

### 列出队列中的项目
```
# salt-run queue.list_items myqueue
- item1
- item2
- item3
```
* 求项目个数
```
# salt-run queue.list_length myqueue
3
```

### 处理队列中的项目
* 弹出第一个项目
```
# salt-run queue.pop myqueue
- item1
```
* 弹出多个项目，例：2个
```
# salt-run queue.pop myqueue 2
- item2
- item3
```
* 弹出一个项目并为它发送一个事件
```
# salt-run queue.process_queue myqueue
- item1
```

### 从队列中删除项目
* 删除一个项目
```
# salt-run queue.delete myqueue item1
True
```
* 删除多个项目
```
# salt-run queue.delete myqueue '["item2", "item3"]'
True
```

[返回目录](../CONTENTS.md)