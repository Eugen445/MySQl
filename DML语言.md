## DML语言

```mysql
数据操作语言

插入:insert

修改:update

删除:delete

#一.插入语句

#方式一:经典的插入
语法:
insert into表名(列名,...) values(值1,...);

#1.插入的值的类型要与列的类型一致或兼容
INSERT INTO beauty(id, `name`, sex, borndate, phone, photo, boyfriend_id)
VALUES(13, '唐艺昕', '女', '1990-4-23', '1111', NULL, 2);

#2.可以为null的列如何插入值?非null的列必须插入值
方式一:插入空
INSERT INTO beauty(id, `name`, sex, borndate, phone, photo, boyfriend_id)
VALUES(13, '唐艺昕', '女', '1990-4-23', '1111', NULL, 2);

方式二:省略
INSERT INTO beauty(id, `name`, sex, borndate, phone, boyfriend_id)
VALUES(13, '唐艺昕', '女', '1990-4-23', '1111', 2);

#3.列的顺序是否可以调换? 可以
INSERT INTO beauty(`name`, sex, id, phone)
VALUES('蒋欣', '女', 16, '2222');

#4.列数和值的个数必须一致

#5.可以省略列明,默认为所有列,而且列的顺序和表中列的顺序一致
INSERT INTO beauty
VALUES(18, '张飞', '男', NULL, '119', NULL, NULL);

#方式二
语法：
insert into 表名
set 列名 = 值, 列名 = 值, ...

INSERT INTO beauty
SET id = 19, `name` = '刘涛', phone = '999';

#两种方式比较

1.方式一支持插入多行,方式二不行
INSERT INTO beauty(`name`, sex, id, phone)
VALUES('蒋欣1', '女', 26, '2222'),
('蒋欣2', '女', 27, '2222'),
('蒋欣3', '女', 28, '2222');

2.方式一支持子查询,方式二不支持
INSERT INTO beauty(id, `name`, phone)
SELECT 37, '宋茜', '3333';

#案例
INSERT INTO my_employees #(Id, First_name, Last_name, Userid, Salary)
VALUE 
(1, 'patel', 'Ralph', 'Rpatel', 895),
(2, 'Dancs', 'Betty', 'Bdancs', 860),
(3, 'Biri', 'Ben', 'Bbiri', 1100),
(4, 'Newman', 'Chad', 'Cnewman', 750),
(5, 'Ropeburn', 'Audrey', 'Aropebur', 1550);

INSERT INTO my_employees 
SELECT 1, 'patel', 'Ralph', 'Rpatel', 895 UNION
SELECT 2, 'Dancs', 'Betty', 'Bdancs', 860 UNION
SELECT 3, 'Biri', 'Ben', 'Bbiri', 1100 UNION
SELECT 4, 'Newman', 'Chad', 'Cnewman', 750 UNION
SELECT 5, 'Ropeburn', 'Audrey', 'Aropebur', 1550; 


#二.修改语句

#1.修改单表的记录

语法:
update 表名
set 列 = 新值, 列 = 新值, ...
where 筛选条件;

#2.修改多表的记录
sql92语法:
update 表1 别名, 表2 别名
set 列 = 值, ...
where 筛选条件
and 筛选条件;

sqlqq语法:
update表1 别名
inner| left | right join 表2 别名
on 连接条件
set 列 = 值,...
where 筛选条件;


#1.修改单表的记录
#案例1:修改beauty表中姓唐的女神的电话为4444

UPDATE beauty
SET phone = '4444'
WHERE `name` LIKE '唐%';	

#案例2:修改boys表中id号为2的名称为张飞,魅力值10

UPDATE boys SET boyname = '张飞', usercp = 10

#2.修改多表的记录
#案例1:修改张无忌的女朋友的手机号为114

UPDATE boys bo
INNER JOIN beauty b
ON bo.`id` = b.`boyfriend_id`
SET b.`phone` = '114'
WHERE bo.`boyName` = '张无忌';

#案例2:修改没有男朋友的女神的男朋友编号为2号

UPDATE boys bo
RIGHT JOIN beauty b ON bo.`id` = b.`boyfriend_id`
SET b.`boyfriend_id` = 2
WHERE bo.`id` IS NULL;

三.删除语句

方式一: delete
语法:

1.单表的删除[*]
delete from 表名 where 筛选条件

2.多表的删除

sql92语法:
delete 删除表的别名
from 表1 别名, 表2 别名
where 连接条件
and 筛选条件

sql99语法

delete 删除表的别名
from 表1 别名
inner| left | right join 表2 别名
on 连接条件
where 筛选条件

方式二:truncate
语法:truncate table 表名;

delete和truncate的区别[面试题]
1.delete 可以加where条件,truncate不能加
2.truncate删除,效率高一丢丢
3.假如要删除的表中有自增长列,如果用delete删除后,在插入数据,自增长列的值从断点开始,
而truccate删除后,在插入数据,自增长列的值从1开始.
4.truncate没有返回值,delete删除有返回值
5.truncate删除不能回滚,delete可以回滚

#案例1:删除手机号以9结尾的女神信息

DELETE FROM beauty
WHERE phone LIKE '%9';

#案例2:删除张无忌的女朋友的信息

DELETE b
FROM beauty b
INNER JOIN boys bo
ON b.`boyfriend_id` = bo.`id`
WHERE bo.`boyName` = '张无忌';

#案例3:删除黄晓明的信息以及他女朋友的信息

DELETE b, bo
FROM beauty b
INNER JOIN boys bo
ON b.`boyfriend_id` = bo.`id`
WHERE bo.`boyName` = '黄晓明';
```



