# 探索Salt SSH
* Salt引入消息队列作为通信传输机制
* Salt与SSH（Secure Shell）理念不同
```
Salt的设计目标是为了一次可以联系数量庞大的远程主机，而SSH设计是每次只和一个交互
```
* 传统的Salt基础设施中，由Minion主动连接Master，Master不需要存储Minion的网络和主机配置；当基于SSH连接时，该规则改变，Master必须通过SSH连接其Minion

## Roster
* Salt SSH引入Roster保存主机信息

### 纯文本Roster
* 通常存储为/etc/salt/roster
* 基本信息
```
host：IP地址或主机名地址
port：SSH默认为22端口
user：运行salt-ssh客户端的默认用户，通常是root
passwd：若使用密码认证，则使用该选项指定密码，如：# salt-ssh --passwd=verybadpass myminion test.ping
sudo：当需要非特权用户执行特权命令时，需要将sudo选项设置为True
priv：当需要带私钥访问Minion时，通过该选项自定义私钥路径
timeout：指定等待SSH连接建立的最大秒数
thin_dir：目标Minion上Salt thin agent安装的目录
```

### 其他内置Roster
* 指定--roster选项
```
# salt-ssh --roster=cloud myminion test.ping
```

## 使用Salt SSH
* salt-ssh命令在使用上和salt命令类似，需要提供target、模块module、方法function和可选参数。
* Salt SSH支持如下target类型：
```
Glob（默认）
Perl兼容正则表达式（-E或--pcre）
列表（-L或--list）
Grain（-G或--grain）
Nodegroup（-N或--nodegroup）
Range（-R或--range）
```
* 指定target类型的方式和salt命令一样：
```
# salt-ssh -G 'os:Ubuntu' test.ping
```

### 使用Saltfile
* 如果在使用Salt SSH时需要指定许多选项，则可以使用Saltfile文件自动添加相应选项

## Salt与Salt SSH
* 两者最主要的不同是：上层通信方式基于底层不同的传输机制架构，salt命令使用消息队列（一对多），而salt-ssh使用SSH（一对一）
* 另一个不同是：性能，Salt SSH非常快，但也有一些额外的开销

## Salt-thin agent
* salt-thin agent的设计目标是：Salt的轻量级版本，能够通过Salt SSH快速复制到远程系统上处理任务；一旦salt-thin打包完成，它会复制到目标系统上，解包然后执行

## 执行thin包
* 执行，以trace日志级别查看运行信息
```
# salt-ssh myminion test.ping --log-level trace
```

### Salt运行状态数据
* 运行状态数据保存在running data目录中
```
# salt-ssh myminion cmd.run 'tree /tmp/.root*/running_data'
```

## 使用原生SSH模式
* Salt SSH在默认模式下使用salt-thin，功能十分强大，但有时只需执行原生SSH命令就可以，使用--raw参数
* 原生模式会忽略掉创建和部署thin包的消耗

[返回目录](../CONTENTS.md)