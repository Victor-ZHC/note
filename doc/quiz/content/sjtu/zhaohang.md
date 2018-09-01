# 招商银行信用卡
## 现场面试
1. 测试中的覆盖
* 结构化覆盖
    * 顶点覆盖
    * 边覆盖
* 主路径覆盖
    * 主路径：长度极大化的简单路径
* 逻辑测试
    * 语句覆盖（把所有判断语句都执行一次）
    * 判定覆盖（把Decision判定的True和False各执行一次）
    * 条件覆盖（把每一个条件的True和False各执行一次）
        * A XOR B, (A=T,B=T) (A=F,B=F), 满足条件覆盖但不满足判定覆盖

## 大数据方向
1. 数据仓库中的拉链表
* 数据仓库经常用历史数据和时间维度做数据分析
* 所谓拉链，就是记录历史，记录某一事物从开始到当前状态的所有变化信息
* 在SQL记录中增加开始时间和结束时间
2. 读文件的300~500行Linux命令
```
cat file | head -n 500 | tail -n +300
sed -n ‘300,500p’ file
```
3. SQL：读各个部门工资最高的人
```
SELECT dep.Name as Department, emp.Name as Employee, emp.Salary 
FROM Department dep, Employee emp 
WHERE emp.DepartmentId=dep.Id 
and emp.Salary=(SELECT max(Salary) FROM Employee e2 WHERE e2.DepartmentId=dep.Id);
```
4. 数据仓库ETL的探索阶段做什么
```
数据仓库中对源数据分析主要有两个阶段：一是数据探索阶段，二是异常数据监测阶段
数据探索阶段包括：
* 收集所有源系统的文档、数据字典等；
* 收集源系统的使用情况；
* 判断数据的起始来源；
* 通过数据概况对原系统的数据关系进行分析
数据探索阶段的主要目的是：理解源系统的情况，为后续的数据建模和逻辑数据映射做准备
```
5. hadoop备份系数dfs.replication
备份系数在hdfs-site.xml中定义，默认值为3.
```
<property>
    <name>dfs.replication</name>
    <value>3</value>
</property>

```

[返回目录](../../CONTENTS.md)