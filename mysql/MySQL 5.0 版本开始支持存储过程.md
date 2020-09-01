MySQL 5.0 版本开始支持存储过程。

存储过程（Stored Procedure）是一种在数据库中存储复杂程序，以便外部程序调用的一种数据库对象。

存储过程是为了完成特定功能的SQL语句集，经编译创建并保存在数据库中，用户可通过指定存储过程的名字并给定参数(需要时)来调用执行。

存储过程思想上很简单，就是数据库 SQL 语言层面的代码封装与重用。

创建储存过程：

 CREATE PROCEDURE select_pub1(userid varchar(32)) BEGIN

 	SELECT

 		* 

​	FROM

​		course_pub 

 	WHERE

​		id = userid;

 

​          END

调用存储过程：

call select_pub1（"参数"）

传入参数

create procedure select_user4(in userid varchar(32),inout usename varchar(32))

begin 

set user

set userid='297e7c7c62b888f00162b8a7dec20000';

select id,name as  username from course_pub where  id=userid;

end

set @userid='297e7c7c62b888f00162b8a7dec20000';

call select_user4(@userid)

create procedure test7(inout userId varchar(32),inout username varchar(32))

begin

​    set userId='297e7c7c62b888f00162b8a7dec20000';

​    set username='';

​    select id,name into userId,username from course_pub where id=userId;

end;

set @uname='';

set @userId='297e7c7c62b888f00162b8a7dec20000';

call test7(@userId,@uname);

select @userId,@uname as username;

 1、传出参数：在调用存储过程中，可以改变其值，并可返回；

​     2、out是传出参数，不能用于传入参数值；

​     3、调用存储过程时，out参数也需要指定，但必须是变量，不能是常量；

​     4、如果既需要传入，同时又需要传出，则可以使用INOUT类型参数

while循环插入1000条数据   

create procedure instert8(username varchar(32))

begin

declare i int default 0;

while(i<1000) do 

begin 

select i;

set i=i+1;

SELECT username;

insert into user1(id,username,sex,age) values(i,username,i,i);

end;

end while;

end ;

call instert8('上的撒')

条件判断if else

 2、实例

  实例1：编写存储过程，如果用户userId是偶数则返回username,否则返回userId

create procedure test7(in userId int)

1. begin
2.   declare username varchar(32) default '';
3.   if(userId%2=0)
4.   then 
5. ​    select name into username from users where id=userId;
6. ​    select username;
7.   else
8. ​    select userId;
9. ​    end if;
10. end;

SELECT name,subject,mark,case when(sex=1) then '男' when(sex=0) then '女' ELSE sex END AS gender  FROM table1  HAVING AVG(mark)>80

select * from table1  where sex>(select sex from table1 where name='李四' GROUP BY name)

select * from users where username  BETWEEN  '李四' and  '柳茵9'

select u.username,u.age,case when(sex=0) then '女' when(sex=1) then '男' else sex end as '性别', r.`partname`  from users u INNER JOIN role r  on u.partId=r.part_id  order by age 

select if(mod(id, 2)= 0, id-1, if(id=( select max(id) from users), id, id+1)) as id from users 

select case when(id%2=0)  then id-1 else(case when id=(select max(id) from users) then id else id+1 end) end as id from users

SELECT

​	p.cat_id,

​	p.parent_cid,

​	p.`name`,

​	p1.cat_id AS id1,

​	p1.parent_cid AS pid1,

​	p1.`name` AS name1,

​	p2.cat_id AS id2,

​	p2.parent_cid AS pid2,

​	p2.`name` AS name2 

FROM

​	`pms_category` p

​	LEFT JOIN pms_category p1 ON p1.parent_cid = p.cat_id

​	LEFT JOIN pms_category p2 ON p2.parent_cid = p1.cat_id 

WHERE

​	p.parent_cid = 0

CREATE UNIQUE INDEX id ON pms_category (id)

select      from pms_category  

1. 查看优化器状态

- - show variables like 'optimizer_trace';

1. 会话级别临时开启

- - set session optimizer_trace="enabled=on",end_markers_in_json=on;

1. 设置优化器追踪的内存大小

- - set OPTIMIZER_TRACE_MAX_MEM_SIZE=1000000;

1. 执行自己的SQL

- - select host,user,plugin from user;

1. information_schema.optimizer_trace表

- - SELECT trace FROM information_schema.OPTIMIZER_TRACE;

1. 导入到一个命名为xx.trace的文件，然后用JSON阅读器来查看（如果没有控制台权限，或直接交由运维，让他把该 trace 文件，输出给你就行了。 ）。

- - SELECT TRACE INTO DUMPFILE "E:\\test.trace" FROM INFORMATION_SCHEMA.OPTIMIZER_TRACE;

**注意：不设置优化器最大容量的话，可能会导致优化器返回的结果不全。**