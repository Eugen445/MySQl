## DDL语言

(数据定义语言)

```mysql
库和表的管理
一.库的管理
创建,修改,删除
二.表的管理
创建,修改,删除

创建:create
修改:alter
删除:drop

#一.库的管理
#1.库的创建

语法:
create database [IF NOT EXISTS] 库名;
CREATE DATABASE IF NOT EXISTS books;

#2.库的修改

#更改库的字符集
ALTER DATABASE books CHARACTER SET gbk;

#3.库的删除

drop database [if exists] 库名;
DROP DATABASE IF EXISTS books;

#二.表的管理
#1.表的创建

create table 表名(
	列名 列的类型 [(长度) 约束],
	列名 列的类型 [(长度) 约束],
	列名 列的类型 [(长度) 约束],
)

CREATE TABLE IF NOT EXISTS book (
	id INT, #编号
	bName VARCHAR(20), #图书名
	price DOUBLE, #价格
	authorId INT, #作者编号
	publishDate DATETIME #出版日期	
) ;

#2.表的修改

alter table 表名 add | drop | modify | change column 列名 [列类型 约束];

#1).修改列名
ALTER TABLE book CHANGE COLUMN publishdate pubDate DATETIME;
#2).修改列的类型和约束
ALTER TABLE book MODIFY COLUMN pubDate TIMESTAMP;
#3).添加新列
ALTER TABLE author ADD COLUMN annual DOUBLE;
#4).删除列
ALTER TABLE author DROP COLUMN annual;
#5).修改表名
ALTER TABLE author RENAME TO book_author;

#3.表的删除

DROP TABLE IF EXISTS book_author;

#通用的写法:

DROP DATABASE IF EXISTS 旧库名;
CREATE DATABASE 新库名;

DROP TABLE IF EXISTS 旧表名;
CREATE TABLE 表名();

#4.表的复制

INSERT INTO author VALUES
(1, '村上春树', '日本'),
(2, '莫言', '中国'),
(3, '冯唐', '中国'),
(4, '金庸', '中国');

#1.仅仅复制表的结构

CREATE TABLE copy LIKE author;

#2.复制表的结构 + 数据

CREATE TABLE copy2
SELECT * FROM author;

#3.只复制部分数据

CREATE TABLE copy3
SELECT id, au_name
FROM author
WHERE nation = '中国';

#4.仅仅复制某些字段

CREATE TABLE copy4
SELECT id, au_name
FROM author
WHERE 1 = 2; #WHERE 0;
```

