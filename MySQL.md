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

