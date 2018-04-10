# 腾讯
1. nginx介绍（负载均衡）
```
1）模块
   a）Handler：处理器模块，直接处理请求；
   b）Filter：过滤器模块，对其他处理器模块输出的内容进行修改；
   c）Proxy：代理类模块，实现服务代理和负载均衡；
2）进程模型
   nginx启动后，会有一个master进程和多个worker进程
   a）master进程，管理worker进程，包括：接收来自外界的信号，向各worker进程发送信号
   b）worker进程，多个worker进程之间是对等的，同等竞争来自客户端的请求，各进程相互独立
```
2. 文件上传
* 使用百度Web Uploader实现，Web Uploader原理：也支持事件机制，比如：on, off，once，trigger
3. SQL索引机制
```
分为：聚集索引和非聚集索引
1）聚集索引：顺序排列，如：一个逐渐自增的表为聚集索引
2）非聚集索引：即：有序目录，一种以空间换时间的方法，如：针对非主键的某一字段添加B+树索引（非聚集索引），则排序后，只需要查询此目录（即：查询B+树）。
   索引存在存储开销和处理开销，适用于查询为主、插入为辅的情况
```
4. CDN
* 内容分发网络（见：阿里前端面试）
5. 快排算法描述
* 递归进行
* 求第500大的O（n）算法，类似快排，分治法解决
6. 状态码
* 302：临时重定向，请求的资源临时从不同的URI响应
* 502：网关或代理服务器从上游服务器收到无效响应
* 504：网关或代理服务器未能从上游服务器收到响应
7. Hibernate的缓存机制
```
包括：
1）一级缓存（session级别）
   事务级缓存，伴随着事务的开启而开启，伴随着事务的关闭而关闭
   session级别的缓存是Hibernate内置的，一定使用
2）二级缓存（sessionFactory级别）
   分为内置缓存和外置缓存
   a）内置缓存：存放映射元数据和预定义SQL语句，内置缓存只读
   b）外置缓存：存储数据库数据的副本，介质：内存或硬盘
3）查询缓存
   加上@Cacheable注解即可
```
* 注：Hibernate延迟加载，只有使用到该对象的数据时才会真正创建
* 注：Hibernate工作原理：
```
1）读取并解析配置文件。
2）读取并解析映射信息，创建SessionFactory。
3）打开Session。
4）创建事物Transaction。
5）持久化操作。
6）提交事务。
7）关闭Session。
8）关闭SessionFactory。
```
* 注：Hibernate检索数据的方式
```
1）利用类间关系：student.getAge()
2）OID检索：Session的get()和load()
3）HQL检索
```
8. DNS
* 主机名与IP地址
* 使用UDP传输
* 域名空间：顶级域名、二级域名、三级域名…
9. Spring拦截器Interceptor原理
```
拦截器：对处理器进行预处理和后处理，是链式调用
实现：继承实现了HandlerInterceptor接口的类，HandlerInterceptor接口中定义了三个方法：
1）preHandle()：处理请求前调用
2）postHandle()：处理请求后调用
3）afterCompletion()：当前Interceptor的preHandle方法返回值为true才执行
```
10. Spring IoC/DI
```
1）IoC：Inversion of Control，控制反转，用于完成对象的创建和依赖注入管理
2）IoC容器的实现原理就是工厂模式+反射机制
注：工厂模式：提供了创建对象的最佳方式
3）java用@interface定义一个注解
4）依赖注入的方式
   a）set注入
   b）构造方法注入
   c）基于注解注入@Autowired
```
11. Spring AOP
* 面向切面编程，将共有的代码全部抽取出来，放置在某个地方集中管理，如：日志记录、事务控制、权限控制等
* （10和11是Spring的两大特征）
12. MyBatis持久层框架
* 支持普通SQL查询、存储过程和高级映射
13. 树的遍历（树是特殊的图）
```
1）广度优先遍历BFS – 图
    BFS() {
  	    输入起始点；
        初始化所有顶点标记；
        初始化一个队列queue并将起始点放入队列；
        while（queue不为空）{
       	    从队列中删除一个顶点s并标记为已遍历； //表示遍历了s
    		将s邻接的所有还没遍历的点加入队列；
  		}
    }
2）深度优先遍历DFS – 图
   分为：中序遍历、前序遍历和后序遍历
```
14. 事务的隔离级别
```
1）Read Uncommitted读未提交
2）Read Committed读已提交
3）Repeatable Read可重复读
4）Serializable可串行化
不考虑隔离性问题（并发问题）：
1）脏读
2）不可重复读：一个事务范围，两个相同查询返回不同数据（由于其他事务的修改操作）
3）幻读：由于其他事务的插入等操作，产生不同的查询结果
```
15. ORM：对象关系映射Object Relational Mapping
* 在编程语言里实现：虚拟对象数据库

[返回目录](../../CONTENTS.md)