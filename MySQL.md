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
