# MySql

### 数据库字段设计原则

1.除非两张表关联字段且不用于显示，原则上两表中字段取名不应该一直，查询语句还得区别名，增加代码量	



如果数据库中的字段类型为char，java中字段类型为boolean的话，会自动转化成true类型

往数据库存一样，如果java字段类型为boolean类型，数据库字段为char类型，则false自动转换为0，true自动转换为1



2.数据库中要区分 减号 和 破折号



1.从一张表中将数据导入到另外一张表

```sql

第一种:

create table dust select * from student;//用于复制前未创建新表dust的情况下

第二种

insert into dust select * from student;//已经创建了新表dust的情况下

----------------------------------------------------------------------

如果表结构不一样

insert into 表1 (列名1,列名2,列名3) select 列1,列2,列3 from 表2

不同数据库，需要在表前面加数据库前缀，database.表名。

注意：以上测试过OK，sql语句不需要在insert后面加 values。

```



### 数据库的时区问题

```mysql
  那我们怎么修改，有两种方法，一种是临时的，一种是长久的。
       一：通过sql命令临时修改

# 设置全局时区 
mysql> set global time_zone = '+8:00';
# 设置时区为东八区 
mysql> set time_zone = '+8:00'; 
# 刷新权限使设置立即生效 
mysql> flush privileges; 
mysql> show variables like '%time_zone%';
 +------------------+--------+
 | Variable_name | Value |
 +------------------+--------+
 | system_time_zone | EST |
 | time_zone | +08:00 | 
 +------------------+--------+
 2 rows in set (0.00 sec)
         二：修改my.cnf实现永久修改

vi /etc/mysql/my.cnf
  然后在mysqld下边的配置中添加一行：

default-time_zone = '+8:00'
  然后重启mysql

service mysql restart
```

