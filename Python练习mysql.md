```
import pymysql


conn = pymysql.connect(host='localhost', port=3306, user='root', passwd='123456', charset='utf8',db='userdb')
curnor = conn.cursor()   

-- 连接数据库，db='userdb'这条参数，能自动执行use userdb; 即进入数据库
-- 前提：本身已经建好了 userdb 这个数据库
-- 通过 curnor 游标发送指令

curnor.execute("show databases")  # 发送指令

result = curnor.fetchall()  # 获得指令结果

print(result)

```
