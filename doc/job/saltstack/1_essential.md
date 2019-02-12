# Salt概览
* Salt是自动化基础框架，是远程执行的典型，允许用户在众多主机上运行命令

## Master和Minion
* Salt基于一主（Master）控制多从（Minion）的思想，通常从Master上发送命令到一组Minion，然后执行命令中的既定任务，最后将执行结果返回到Master

## Targeting Minion
* Salt的每个远程执行都需要指定一个匹配的target，即：进行执行的Minion

## Salt命令
* 在所有通配的Minion上执行test.ping命令：
```
# salt '*' test.ping
```
* 通过正则表达式指定多个Minion，-E即--pcre，例：
```
# salt -E '^[mM]in.[eou]n$' test.ping 
```
* 通过逗号分隔列表指定多个Minion，-L即--list，例：
```
# salt -L web1,web2,db1,proxy1 test.ping
```
* 通过指定一个IPv4地址或CIDR（无类域间路由）子网来指定Minion，-S即--ipcidr，例：
```
# salt -S 192.168.0.42 test.ping
# salt -S 192.168.0.0/16 test.ping
```
* 通过操作系统、CPU架构等以 **键值对（:分隔）** 形式指定Minion，-G即--grain，例：
```
# salt -G 'os:Ubuntu' test.ping
# salt -G 'os_family:Debian' test.ping
```
* 混合指定，-C即--compound，混合target在前面加上类型简写和@符号，类型简写如下表：

|简写|target|
|-----------|:---------:|
|G|Grain|
|E|PCRE Minion ID|
|P|Grain PCRE|
|L|列表|
|I|Pillar|
|S|子网/IP地址|
|R|SECO范围|

例：
```
# salt -C 'G@os:Ubuntu,I@role:web,S@192.168.100.0/24' test.ping
```
另，布尔类型的与（and）、或（or）、非（not）也可使用：
```
# salt -C 'min* or *ion' test.ping
```
* 通过节点组定义，如在配置文件提前定义nodegroups，命名为：webdev，-N即--nodegroup，例：
```
# salt -N webdev test.ping
```

## 运行模块方法
* Salt命令中，模块方法紧随target，格式如下：
```
salt <target> <模块名>.<方法> [参数...]
```
例：
```
# salt '*' test.echo 'Hello world'
```

### salt核心模块及重要方法
* test.ping：仅返回True，用于检测Minion是否可响应
* test.echo：使Minion显示出传递给自己的字符串
* test.sleep：使Minion先sleep若干秒后再返回True
* test.version：使每个Minion返回其salt版本
* pkg.install：安装软件包
* pkg.remove：卸载软件包
* file.replace：查找替换文件
* sys.doc：显示执行模块中公共方法的自述文档

## SLS文件树
* SLS指代SaLt State，是Salt中常用的文件结构，采用键值对设计：每项都有唯一的键、引用一个值

### top.sls文件
* State和Pillar系统中都有名为top.sls的文件，指定在什么环境为哪些Minion提供哪些执行文件

### 使用State进行配置管理
* /srv/salt目录下的文件用于定义Salt State，强制Minion处于某一状态（State）：X软件包（package）需要安装，文件（file）Y格式正确，服务（service）Z开机自启并处于运行状态，如下：
```
apache2:
  pkg:
    - installed
  service:
    - running
  file:
    - managed
    - name: /etc/apache2/apache2.conf
```

### 使用include块
* 替换内容

### 使用requisite排序
* require：强制State等待列表中定义的State都成功执行
* watch：强制State在项目变更时执行指定动作
* use：使用use的State不会将requisite继承过来
* prereq：只有在另一个State预计会变更时才会需要运行

### 反转requisite
* require_in：表示State X is required by State Y

### 扩展SLS文件
* extend：对引入的State进行修改

## Grain、Pillar及模块基础
* Grain和Pillar均是用户自定义变量的方案，区别：
1. Grain定义在指定的Minion上，Pillar定义在Master上
2. Grain通常用于不常修改的数据，Pillar通常用于动态数据

### 使用Grain获取Minion特征数据
* Grain在启动时进行加载，缓存在内存中，提升性能
* 通过grains.items方法查看Minion的Grain数据，例：
```
# salt myminion grains.items
```
* 通过grains.setval方法在Grain文件中添加或修改Grain，例：
```
# salt myminion grains.setval mygrain "the content"
```

### 使用Pillar使变量集中化
* Pillar的top.sls文件在配置和功能上与State的top.sls文件一致：首先声明一个环境，然后是一个target，最后是该target需要使用的SLS文件列表
* 通过pillar.items查看所有Pillar数据，例：
```
# salt myminion pillar.items
```

[返回目录](../CONTENTS.md)