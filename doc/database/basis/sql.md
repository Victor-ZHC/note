# SQL

## join
表格student1
|id|name|
|:---|:---|
|1|张三|
|2|李四|
|3|王五|
表格student2
|id|course_name|
|:---|:---|
|1|数学|
|2|英语|
|3|数学|
|4|计算机|
* 内连接也即自然连接
```
select * from student1 natural join student2;
```
|id|name|course_name|
|:---|:---|:---|
|1|张三|数学|
|2|李四|英语|
|3|王五|数学|
* 左外连接(以左表为主表)
```
select * from student1 left join student2 on student1.id = student2.id;
```
|id|name|id|course_name|
|:---|:---|:---|:---|
|1|张三|1|数学|
|2|李四|2|英语|
|3|王五|3|数学|
* 右外连接(以右表为主表)
```
select * from student1 right join student2 on student1.id = student2.id;
```
|id|name|id|course_name|
|:---|:---|:---|:---|
|1|张三|1|数学|
|2|李四|2|英语|
|3|王五|3|数学|
|NULL|NULL|4|计算机|

## 存储过程和函数
* 区别
    * 存储过程一般独立执行，函数可以作为查询语句的一部分
    * 存储过程实现复杂的判断，函数一般简单
    * 存储过程创建时就在服务器完成了编译，执行速度比函数快
* 存储过程
```
//drop procedure sp1 如果存储过程一存在，则删去
delimiter //						  
create procedure sp1()					 
begin 
        declare done integer default 0;

        declare mystuid varchar(15);
        declare optFir char(15);
        declare optFirSco integer;

        declare stuFirNum integer;
        declare higherFirNum integer;

        declare cur cursor for select stuid, optionalFir, optionalFirSco from score;

        open cur;

        repeat
            fetch cur into mystuid, optFir, optFirSco;
            if not done then

	            select count(*) into stuFirNum from score sc where sc.optionalFir = optFir;
                select count(*) into higherFirNum from score sc where (sc.optionalFir = optFir and optFirSco < sc.optionalFirSco); 
 
                if(higherFirNum < floor(0.05*stuFirNum)) then
                    update score set optionalFirLev = 'A+' where stuid = mystuid;
                end if;

            end if;
       until done end repeat;

       close cur;						  
end;

调用存储过程：
call sp1();
```
* 函数
```
create function NthSalary(d_name varchar(20), N int)
returns int
begin
...
end;
```

## 触发器
* 分为事前触发和事后触发
```
create trigger score_trigger_insert before insert on score 
    for  each  row  
begin
...
end;
```

## Union和Union All
* 要求两个表格有相同数目的列，并且有相似的数据类型
* Union是去重合并，Union All不去重