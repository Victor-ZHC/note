# Salt Cloud进阶

## Salt Cloud配置
### 全局配置
* Salt Cloud基础配置通常配置在主配置文件中，路径为：/etc/salt/cloud
* Salt Cloud遵循自上而下的配置，配置文件中定义每种类型的配置都会继承到下一级配置，除非进行覆盖操作。操作的顺序如下：
```
1. /etc/salt/cloud
2. Provider配置
3. Profile配置
4. cloud map
```
* provider和profile配置块在Salt配置中需要保证唯一性

### Provider配置
* Provider对应的是：允许创建新的计算实例的云主机公司，存储在：/etc/salt/cloud.providers文件或者/etc/salt/cloud.providers.d/目录下

### Profile配置
* Profile配置用于构建配置块，最终定义某一类型的计算实例，存储在：/etc/salt/cloud.profiles文件或者/etc/salt/cloud.profiles.d/目录下

## 构建自定义部署脚本
### Salt Bootstrap脚本
* Salt Cloud在非Windows计算实例上安装Salt时，默认采用Salt Bootstrap脚本进行部署
* 要求Salt Cloud更新Bootstrap：
```
# salt-cloud --update-bootstrap
```

### 定制部署脚本
* 部署脚本通常处理如下任务：
```
1. 在Minion上自动放置已签名的key
2. 放置Minion配置文件
3. 为操作系统安装Salt Minion包
4. 启动salt-minion服务
```

### 给脚本传递参数
* Salt Cloud允许在Salt Cloud的配置文件中通过script_args参数来传递参数，相应参数可以应用在目标Minion、Provider和Profile等中

### 使用文件映射
* file_map变量是一个字典，能够添加用于Minion的任何相关的配置文件，字典中的每一个键名（key）对应的是需要上传的本地的文件名，值（value）对应需要上传到的远端路径名

## cloud映射
* cloud映射允许一次性指定一组主机，用于创建主机组
* 使用映射：
```
# salt-cloud -m /etc/salt/cloud.maps.d/mymap.map
```
* 使用映射并行创建机器：
```
# salt-cloud -P -m /etc/salt/cloud.maps.d/mymap.map
```

## 构建自动伸缩的反应器
### Cloud缓存
* Salt Cloud会保存两类缓存（cache），其中一个是其他缓存的索引文件，通常缓存目录为：/var/cache/salt/cloud

### 使用Cloud缓存事件
* Cloud缓存事件可以用于联合自动伸缩系统

### 捕捉Cloud缓存事件
* 一旦Cloud配置完成，如果Cloud缓存发生变化就发送事件，则可以建立一个反应器（Reactor）来响应事件
* 当Salt Cloud使用--profile或--map参数来请求创建计算实例后，Salt Cloud会进行如下操作：
```
1. 请求对应的云供应商创建一个计算实例
2. 等待计算实例可用后的IP地址
3. 等待该IP地址上的SSH/SMB服务可用
4. 向该IP地址上传文件
5. 执行部署脚本或Windows安装器
6. 清除临时脚本
7. 返回给用户
```

[返回目录](../CONTENTS.md)