## DML语言

```
数据操作语言

插入:insert

修改:update

删除:delete

#一.插入语句

#方式一:经典的插入
语法:
insert into表名(列名,...) values(值1,...);

#1.插入的值的类型要与列的类型一直或兼容
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
set 列名 = 值, 列明 = 值, ...

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


#二.修改语句

#1.修改单表的记录

语法:
update 表名
set 列 = 新值, 列 = 新值, ...
where 筛选条件;

#2.修改多表的记录



#1.修改单表的记录
#案例1:修改beauty表中姓唐的女神的电话为4444

UPDATE beauty
SET phone = '4444'
WHERE `name` LIKE '唐%';	

#案例2:修改boys表中id号为2的名称为张飞,魅力值10

UPDATE boys SET boyname = '张飞', usercp = 10

#2.修改多表的记录
```



