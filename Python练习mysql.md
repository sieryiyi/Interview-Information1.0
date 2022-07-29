技巧：
    print("用户名：{}，密码：{}".format(1,2))
    >>>用户名：1，密码：2

### 练习1
```
import pymysql

conn = pymysql.connect(host='localhost', port=3306, user='root', passwd='123456', charset='utf8')
curnor = conn.cursor()

# 通过 curnor 游标发送指令
# 建表

curnor.execute("use try1")

sql = """                                           ------------ 一般会先将所需要的语句拼成sql语句，再去运行
CREATE TABLE student ( 
	id INT  auto_increment PRIMARY KEY,
	name VARCHAR ( 16 ) NOT NULL, 
	email VARCHAR ( 16 )  NULL,
	age INT NULL 

) DEFAULT CHARSET = utf8;
"""

curnor.execute(sql)  # 建表
conn.commit()

curnor.execute("show tables")  # 查看数据库下的所有表
print(curnor.fetchall())

curnor.execute("desc student")  # 查看表的详细信息
print(curnor.fetchall())

curnor.execute("drop table student")  # 删除表
conn.commit()

```
### 练习2：用户管理系统

```
# 用于练习mysql在Python下的使用

# 学生信息管理系统

import pymysql

conn = pymysql.connect(host='localhost', port=3306, user='root', passwd='123456', charset='utf8')
curnor = conn.cursor()

# 通过 curnor 游标发送指令
# 建表

curnor.execute("use try1")

sql = """
CREATE TABLE user ( 
	id INT  auto_increment PRIMARY KEY,
	name VARCHAR ( 32) ,
	password VARCHAR ( 64 ) 

) DEFAULT CHARSET = utf8;
"""

curnor.execute(sql)  # 建表
conn.commit()

curnor.execute("show tables")  # 查看数据库下的所有表
print(curnor.fetchall())

name = '123'

password = '666'

sql = 'insert into user (name,password) values ("{}","{}")'.format(name, password)  # 添加数据
curnor.execute(sql)
conn.commit()

curnor.execute("desc user")  # 查看表的详细信息
print(curnor.fetchall())

sql='select * from user where name="{}" and password="{}"'.format(name,password)  #查询数据
curnor.execute(sql)
result=curnor.fetchall()
print(result)

curnor.execute("drop table user")  # 删除表
conn.commit()

```


