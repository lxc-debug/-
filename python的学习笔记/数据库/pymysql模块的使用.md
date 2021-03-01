## pymysql模块的使用,事务以及数据备份

#### 1.pymysql模块

+ ##### 查询

```python
import pymysql

coon = pymysql.connect(host='127.0.0.1'
                      user='root'
                      password='123'
                      database='homework')

cur = coon.cursor		#这个是数据会以元组的形式返回
#cur = coon.cursor(cursor=pymysql.cursors.DictCursor)	#这个是数据会以字典的形式返回
try:
	cur.execute('select * from student')		#在这里可以不用加;因为函数内部会自动加
	ret=cur.fetchone()		#会返回一条数据
	print(ret)
	ret=cur.fetchmany(10)	#会返回十条数据
	print(ret)
	ret=cur.fetchall()		#会返回余下的所有数据
	print(ret)
except pymysql.err.ProgrammingError as e:
    print(e)		#个人感觉这一步是为了简化报错，防止报错后需要看大段的内容
cur.close()
conn.close()
```

+ ##### 增删改

```python
import pymysql

coon = pymysql.connect(host='127.0.0.1'
                      user='root'
                      password='123'
                      database='homework')

cur = coon.cursor		

try:
    cur.execute('insert into student values(18,"男",3,"大壮")')
    cur.execute('update student set gender="女" where sid = 1')
    coon.commit()	#在做增删改的时候，需要进行commit才会在硬盘进行修改
except:
    conn.roolback()			#一旦发生异常，那么整个try的内容就全部都会清理掉，不做提交

cur.close()
conn.close()
    
```

+ ##### 防止sql注入的一种方法

```python
import pymysql

coon = pymysql.connect(host='127.0.0.1'
                      user='root'
                      password='123'
                      database='day42')

cur = coon.cursor
user=input('username:')
password=input('passowrd:')
sql='select * from userinfo where user= %s and password =%s'
cur.execute(sql,(user,password))#使用这种方式就可以避免sql注入的问题

#'select * from userinfo where user = "1869" or 1=1;--“and password = "3714" '一旦自己使用字符串进行拼接，就会产生问题，比如上式，--是注释掉的意思，
也就是用户输入1869" or 1=1;--字段就会产生问题，而使用execute函数就会避免这个问题
```

#### 2.事务以及数据的备份

+ ##### 数据锁

```python
begin:
select age from userinfo where id =1 for update
#这里的for update是告诉程序接下来要进行一个update的操作
update userinfo set age =85 where id =1
commit;
#相当于加了一个数据锁，没有commit之前，其他的程序不能访问这一条数据。
```

+ ##### 数据的备份

```python
1.备份库中的所有的表
myspldump -uroot -p123 -h127.0.0.1 homework > D:\python_22\day42\tmp.sql

还原数据
source D:\python_22\day42\tmp.sql#在哪个库下执行就会备份到哪一个库中
2.备份一整个库
myspldump -uroot -p123 -h127.0.0.1 --databases homework > D:\python_22\day42\tmp.sql	#将整个库都备份了
    
source D:\python_22\day42\tmp.sql	#还原一整个库
```

