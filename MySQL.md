https://www.bilibili.com/video/BV15R4y1b7y9?spm_id_from=333.999.0.0&vd_source=07999cb1d010fa9357b6650a0ee711a7

# MySQL数据库

### 1、安装、配置、启动

Navicat：专门为 MySQL 设计的可视化数据库 GUI 管理工具（一般公司不用）

### 2、数据库命令（Navicat）
```
SHOW DATABASES; -- 查看所有数据库

CREATE DATABASE try1;-- 创建数据库

DROP DATABASE try1;-- 删除数据库

USE try1;-- 进入数据库

SHOW TABLES;-- 查看当前数据库的表

```

### 3、数据库命令（python）

如果在Python下使用：需要用到 pyMySQL 包，与数据库进行连接

简单来说！！！Python通过这个包，与数据库进行连接，通过这个连接，发送过去数据，那边数据库处理完了，会返回一个结果，得接收一下这个结果，才能在Python里输出，如下面的 show databases 操作

```
import pymysql

conn = pymysql.connect(host='localhost', port=3306, user='root', passwd='123456', charset='utf8')
curnor = conn.cursor()

# 通过 curnor 游标发送指令

curnor.execute("show databases")  # 发送指令

result = curnor.fetchall()  # 获得指令结果

print(result)

```

另一点！！！在Python中，如果想对数据库进行 新增、删除、修改 操作，则需要额外加一个命令语句，如下！！！

```
curnor.execute("create database try1")
conn.commit()  # 注意这句话！

curnor.close()
conn.close()  # 关闭数据库

```

### 4、数据表命令

##### 创建表结构

--------------- 一张表一般只能有一个自增列！！！一般是主键-------------------
```
CREATE TABLE 表名(

	列名 类型，
	列名 类型
	) DEFAULT CHARSET=utf8;
```
例如：
```
USE try1;
CREATE TABLE tb2 ( 
	id INT PRIMARY KEY,           -- 设置主键，不允许为空，不允许重复
	NAME VARCHAR ( 16 ) NOT NULL, -- 长度等于16的字符串类型，不允许为空
	age INT NULL,                 -- 允许为空（默认）
	lenth INT DEFAULT 3           -- 如果未插入数据，默认值：3
) DEFAULT CHARSET = utf8;

```

注意，主键不能重复，需要人为维护，非常麻烦！！！所以一般把主键+自增结合起来，如下-----------

有了自增auto_increment后，可以在添加数值的时候不给主键的值

```
USE try1;
CREATE TABLE tb2 ( 
	id INT NOT NULL auto_increment PRIMARY KEY     -- 设置主键+自增
	          
) DEFAULT CHARSET = utf8;

```

##### 主键作用

1、约束，让每一条数据的主键都是不重复的

2、加速查找，根据主键找，可以很快的找到数据

##### 改、删

```
USE try1;
CREATE TABLE tb2 ( 
	id INT  auto_increment PRIMARY KEY,       -- 主键，不允许为空，不允许重复
	NAME VARCHAR ( 16 ) NOT NULL,             -- 长度等于16的字符串类型，不允许为空
	age INT NULL,                             -- 允许为空（默认）
	lenth INT DEFAULT 3                       -- 如果未插入数据，默认值：3
) DEFAULT CHARSET = utf8;


ALTER TABLE tb2 add age2 INT;                    -- 添加列（列名、类型，也可以在后面继续加是否默认等等）

ALTER TABLE tb2 DROP COLUMN age2;                -- 删除列（drop后面跟列名）

ALTER TABLE tb2 MODIFY COLUMN age VARCHAR( 16 ); -- 修改age列的类型为char类型(修改类型）也可以修改约束


ALTER TABLE tb2 CHANGE age age INT DEFAULT 5; 
-- 修改列名+类型，语法是change 原列名，新列名，新类型，以及后续可选的一些操作，如设置默认值、自增、允许为空等


ALTER TABLE tb2 ALTER age SET DEFAULT 3;  -- 修改默认值

ALTER TABLE tb2 ALTER age DROP DEFAULT;   -- 删除默认值

DESC tb2;                                 -- 查看表

DELETE FROM tb2;                          -- 清空表

DROP TABLE tb2;                           -- 删除表

```

change 和 modify 区别，modify不能修改列名


### 5、数据类型

##### 整型

	tinyint：表示小的整数，-128~127，想无符号就在后面加个 unsigned

	bigint：表示大的整数

	INT：有符号

	INT unsigned：无符号数字

	int (5) zerofill：整型如果不足5位，自动在前面补零

##### 小数类型

	decimal(8,2) -- 其中，8表示数字整个的长度，2表示小数点后面的长度，如果超了，会自动四舍五入
	
##### 字符串类型

	varchar(3)：变长的字符串
	
	char(3)：定长的字符串，二者主要在底层体现区别，如varchar（3）插入了一个长度为 1 的字符串，则底层存储		    空间是1，而char固定为3

### 6、插入数据操作

```
INSERT INTO tb2(id,age) VALUES(0,5);   -- 在表中插入一条数据，注意，不允许为空的列，一定要给它赋值，允许为空的可以在插入过程中不提到，id由于是自增的，虽然这里给了0，但显示上会是1，再给一条0，会显示id=2

DESC tb2;           -- 查询表的配置信息

SELECT * FROM tb2;  -- 查询表的详细数据信息
```

### 7、关于时间的数据列

##### ①、datetime（存多少显示多少）

	开发中用的多

##### ②、timestamp

	跟时区有关系


### 8、对数据行进行增删改查

##### ①、插入数据

可以多行插入，即values后面多跟几个括号

```
	insert into 表名（列名1，列名2....） values（数据1，数据2.....）（数据1，数据2......）；
```
##### ②、删除数据

```
delete from 表名；

delete from 表名 where 条件；

如 delete from 表名 where name="123" and id＞1；也可以是or 或者大于号小于号等等

```

##### ③、修改数据

```
updata 表名 set 列名=值；

如：update tb2 set age=age+1 where id=2;

    update tb2 set name=concat(name,"123") where id=2;  --- concat函数，拼接字符串
```

##### ④、查询数据
```
select * from tb2;
select id ,name  from tb2;

select id ,name ,111 from tb2;  -- 查询出来的结果除了ID，name列，还会固定有一个111列
select id ,name ,111 as age from tb2;  -- 在上面的基础，将111列显示为age列，但其中的数据还都是111

select id ,name  from tb2 where 条件;

### 9、sql语句的安全问题

不要用format 拼接语句，不然如果用户名输入的是' or 1=1 --，则拼接后会变成select * from tb1 where name ='' or 1=1 -- password='123

后面--后的会被当成注释注释掉，这种情况，即使用户名是错的，也可以查看数据库中的所有信息

改进方法：
```
	curnor.execute("select * from user where name=%s and password=%s",[123,456])
	result=curnor.fetchall()
	print(result)
```
