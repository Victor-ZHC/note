# 深入Salt内部

## Salt缓存

### Master任务缓存
* jobs/目录默认存储所有Master执行的任务数据，目录采用分片hash模式产生

### Master端的Minion缓存
* 一旦Salt开始执行任务，缓存目录下会产生名为minions/的缓存目录，该目录包含以每个Minion ID命名的子目录，用于存放Minion的缓存数据

### Minion端的proc/目录
* proc/目录维护当前Minion正在运行的任务数据

## 渲染器

* Salt内建了渲染器系统，可以将各式各样的格式渲染成Salt可使用的结构

### 渲染SLS文件
* 默认情况下，Salt中的所有SLS文件会渲染两次：首先通过Jinja模块引擎渲染；然后使用PyYAML类库进行渲染。

## 加载器
* 加载器系统（Loader System）是Salt运作的核心，简言之，Salt就是一个模块收集器，使用加载器收集模块并绑定在一起。

### 执行模块
* Salt设计的初衷就作为远程执行系统，添加到加载器的大多数模块类型都是用于扩展远程执行功能的
* runner模块和执行模块最重要的区别是：runner模块的设计是在Master上运行，而执行模块的设计是在远端的Minion上运行

## 深入State编译器
```
命令式编程：如同一个脚本：执行任务A，待完成后，执行任务B；B完成后执行任务C
声明式定义：典型的是面向对象编程，基本理念是：用户声明哪些任务需要执行，然后软件按照它们适合的顺序进行执行。Puppet本质上是声明式配置管理系统。
```
* Salt是唯一一个支持命令式顺序以及声明式执行的系统。若没有定义依赖，默认Salt按照SLS文件中定义的顺序执行State；若一个State因为需求的任务在之后才出现而导致运行失败，则完成整个任务需要Salt运行多次

## High State与Low State
* High数据一般指用户可见的数据；Low数据一般指被Salt提取并使用的数据
* High State数据可以通过state.show_highstate查看：
```
# salt myminion state.show_highstate --out yaml
```
* Low State数据可以通过state.show_lowstate查看：
```
# salt myminion state.show_lowstate --out yaml
```

## 实行State化
* State模块总是需要一个名称（name）
* State模块总是返回如下数据格式：
```
name：当State执行结果返回给用户时，name用于识别被评估的State
result：只返回True（执行成功）或False（执行失败）或None
changes：只出现在result返回值为True的时候，表示系统中资源达到需要的配置过程中进行了哪些变更
comment：表示附加信息
```

[返回目录](../CONTENTS.md)