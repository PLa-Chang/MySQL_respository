* # 创建用户

  我们现在默认使用的都是`root`用户，超级管理员，拥有全部的权限。但是，一个公司里面的数据库服务器上面可能同时运行着很多个项目的数据库。所以，我们应该可以根据不同的项目建立不同的用户，分配不同的权限来管理和维护数据库。

  ## 创建用户

  > CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';

  - `用户名`：将创建的用户名
  - `主机名`：指定该用户在哪个主机上可以登陆，如果是本地用户可用`localhost`，如果想让该用户可以从任意远程主机登陆，可以使用通配符%
  - `密码`：该用户的登陆密码，密码可以为空，如果为空则该用户可以不需要密码登陆服务器

  例子：

  ```sql
  ‐‐ user1用户只能在localhost这个IP登录mysql服务器
  CREATE USER 'user1'@'localhost' IDENTIFIED BY '1234';
  ‐‐ user2用户可以在任何电脑上登录mysql服务器
  CREATE USER 'user2'@'%' IDENTIFIED BY '1234';
  ```

  ## 授权

  用户创建之后，没什么权限,需要给用户授权

  > GRANT 权限1, 权限2... ON 数据库名.表名 TO '用户名'@'主机名';

  - `GRANT` 授权关键字
  - 授予用户的权限，如`SELECT`，`INSERT`，`UPDATE`等。如果要授予所有的权限则使用`ALL`
  - `数据库名.表名`：该用户可以操作哪个数据库的哪些表。如果要授予该用户对所有数据库和表的相应操作权限则可用*表示，如`*.*`
  - `'用户名'@'主机名'`: 给哪个用户授权

  例子：

  1. 给`user1`用户分配对`test`这个数据库操作的权限

  ```sql
  GRANT CREATE,ALTER,DROP,INSERT,UPDATE,DELETE,SELECT ON test.* TO 'user1'@'localhost';
  ```

  2. 给`user2`用户分配对所有数据库操作的权限

  ```sql
  GRANT ALL ON *.* TO 'user2'@'%';
  ```

  ## 撤销授权

  > REVOKE 权限1, 权限2... ON 数据库.表名 FROM '用户名'@'主机名';

  例子：

  撤销user1用户对test操作的权限

  ```sql
  REVOKE ALL ON test.* FROM 'user1'@'localhost';
  ```

  ## 查看权限

  > SHOW GRANTS FOR '用户名'@'主机名'; 

  例子：

  查看`user1`用户的权限

  ```mysql
  SHOW GRANTS FOR 'user1'@'localhost';
  ```

  ## 删除用户

  > DROP USER '用户名'@'主机名';

  例子：

  ```mysql
  DROP USER 'user2'@'%';
  ```

  # 修改密码

  ## 修改管理员密码

  > mysqladmin -uroot -p password 新密码 
  >
  > -- 新密码不需要加上引号
  >
  > -- 注意：需要在未登陆MySQL的情况下操作。

  例子：

  ```mysql
  mysqladmin ‐uroot ‐p password 123456
  输入老密码
  ```

  ![](E:\work\notes\19.mysql\img\password.png)

  ## 修改普通用户密码

  > set password for '用户名'@'主机名' = '新密码';
  >
  > -- 注意：需要在登陆MySQL的情况下操作。

  ```mysql
  set password for 'user1'@'localhost' = '666666';
  ```

  

|  数据类型名称   |                             描述                             |
| :-------------: | :----------------------------------------------------------: |
|    SMALLINT     | 小的整数，带符号的范围是-32768到32767.无符号的范围是0到65535 |
|    MEDIUMINT    |          中等大小整数-8388608到8388607，0到16777215          |
| **INT/INTEGER** |  普通大小的整数，-2147483648到2,147,483,647，0到4294967295   |
|     BIGINT      | 大整数，-9223372036854775808到9223372036854775807，0到18446744073709551615 |
|      FLOAT      | 小(单精度)浮点数，允许的值-3.402823466E+38到-1.175494351E-38,0和1.175494351E-38到3.402823466E+38,这些是理论限制，基于IEEE标准。实际的范围根据硬件或操作系统的不同可能稍微小些 |
|   **DOUBLE**    | 普通大小(双精度)浮点数，允许的值-1.7976931348623157E+380到-2.2250738585072014E-308,0和2.2250738585072014E-38到 1.7976931348623157E+308.这些事理论限制，基于IEEE标准。实际的范围根据硬件或操作系统的不同可能稍微小些 |
|    **DATE**     | 日期，支持的范围为‘1000-01-01’到‘9999-12-31’，MySQL以'YYYY-MM-DD'格式显示DATE值，但允许使用字符串或数字为DATE列分配值 |
|  **DATETIME**   | 日期和时间的组合。支持的范围是‘上面加上00：00：00’到‘上面第二个加上23：59：59’.MySQL以YYYY-MM-DD HH:MM:SS“格式显示DATETIME值，但允许使用字符串或数字为DATETIME列分配值 |
|  **TIMESTAMP**  |         时间戳，范围是'1970-01-01 00:00:00'到2037年          |
|    **TIME**     | 时间，范围是‘-838：59：59’到‘838：59：59’.MySQL以‘HH:MM:SS’格式显示TIME值，但允许使用字符串或数字为TIME列分配值 |
|      YEAR       | 两位或四位格式的年。默认是四位格式。在四位格式中，允许的值是1901到2155和0000.在两位格式中，允许的值是70到69，表示从1970到2069年。MySQL以yyyy格式显示YEAR值，但允许使用字符串或数字为YEAR列分配值 |
|     CHAR(M)     | 固定长度字符串，当保存时在右侧填充空格以达到指定长度。M表示列长度。M的范围是0到255个字符 |
| **VARCHAR(M)**  | 变长字符串。M表示最大列长度。M的范围是0到65535.（VARCHAR的最大实际长度由最长的行的大小和使用的字符集确定。最大有效长度是65355字节） |
|    BLOB[(M)]    | 最大长度为65535(216-1)字节，=的BLOB列，可以给出该类型的可选长度M。如果给出，则MySQL将列创建为最小的但是足以容纳M字节长度的值的BLOB类型 |
|    TEXT[(M)]    | 长字符串，最大长度为65535(216-1)字符的TEXT列。可以给出可选长度M。则MySQL将列创建为最小的但是足以容纳M字符长度的值的TEXT类型。 |

## 查看表结构

```mysql
-- 查看表结构
DESCRIBE dept;
DESC dept;
```

![QQ截图20191106200120](E:\work\notes\19.mysql\img\QQ截图20191106200120.png)



练习：

创建一张`user`表, 可以存储以下内容：姓名，性别，年龄，生日，电话，家庭住址，邮箱

```shell
	CREATE TABLE `user`(
		`name` VARCHAR(20) COMMENT '姓名',
		`gender` CHAR(1) COMMENT '性别',
		`age` INT COMMENT '年龄',
		`birthday` DATE COMMENT '生日',
		`phone` VARCHAR(20) COMMENT '电话',
		`address` VARCHAR(50) COMMENT '住址',
		`email` VARCHAR(20) COMMENT '邮箱'
	);
```



## 创建和某表结构一样的表

```mysql
-- 创建和dept结构一样的表
CREATE TABLE d LIKE dept;

-- 创建表
CREATE TABLE t AS select * from dept;
```

## 删除表

```mysql
DROP TABLE table_name
```

## 添加列

```mysql
ALTER TABLE d ADD id INT;
```

## 修改列属性

```mysql
ALTER TABLE d MODIFY id VARCHAR(20);
```

## 修改列名

```mysql
ALTER TABLE d CHANGE id ss VARCHAR(20);	
```

## 删除列

```mysql
ALTER TABLE d DROP ss;
```

## 重命名表

```mysql
RENAME TABLE d TO dd;
```



# CRUD操作

* 对数据表中的数据操作通常有添加(Create)、查询(Retrieve)、修改(Update)、删除(Delete)、简称为CRUD。

## 添加数据



**INSERT INTO table_name VALUES(值列表)**

**INSERT INTO table_name (列列表) VALUES(值列表)**

```mysql
-- 不推荐使用
INSERT INTO dept VALUE(1,'研发部');
-- 2
INSERT INTO dept VALUES(2,'销售部');
INSERT INTO dept VALUES(3,'行政部'),(4,'技术部');
-- 3
INSERT INTO dept(deptno,deptname)VALUES(5,'安保部');
```

区别：

* value和values的区别，values可以同时插入多条数据用逗号隔开
* dept和dept(列名，列名。。。)区别，如果不写列表必须按照列表创建时的顺序每一列都要添加
* 有列名的按照列名排列顺序添加

## 查询数据

```mysql
-- 查询所有数据
SELECT *FROM dept;
-- 查询某列的数据
SELECT deptname FROM dept;
-- 根据条件查询*
SELECT deptno FROM dept WHERE deptname='销售部';
```

## 修改数据

```mysql
--全部修改为6
UPDATE dept SET deptno=6;
--根据条件修改
UPDATE dept SET deptno=1 WHERE deptname='研发部';
UPDATE dept SET deptno=2 WHERE deptname='销售部';
UPDATE dept SET deptno=3 WHERE deptname='行政部';
UPDATE dept SET deptno=4 WHERE deptname='技术部';
UPDATE dept SET deptno=5 WHERE deptname='安保部';
```

## 删除数据

```mysql
-- 删除数据 ,一定要加 where 条件
DELETE FROM dept WHERE deptno=5;
-- 全部删除
DELETE FROM dept;
-- 清空/截断 所有数据(慎用)
TRUNCATE TABLE dept;
```

区别

* delete from dd;
* truncate table dd;
* delete 是清空表中的数据,`DML`
* truncate 是清空表数据（删除表后重新创建一个一样表），`DDL`

## where条件连接

当`sql`语句中的条件有多条时，可以将多个条件连接起来。他们之间的关系有一下几种：

**`and`**

   `a and b`: 表示 需要同时满足 a 条件 和 b 条件

**`or`**

​	`a or b`: 表示 满足 a 条件 或 b 条件都可以

`in`

​	`in(a, ... ,b)`： 表示在 a 及 b 这些值中都可以

`like`

​    模糊查询,  % 表示任意个字符  _ 表示一个字符

# 数据备份和还原

## 命令行备份

### 备份结构

1.备份表结构

```shell
mysqldump -u root -p -d dbname table1 table2 ... > a.sql
```

2.备份数据库的所有表结构

```shell
mysqldump -u root -p -d dbname > b.sql
```

3.备份多个数据库的所有表结构

```shell
mysqldump -u root -p -d --databases db1 db2... > c.sql
```

4.备份所有数据库的表结构

```shell
mysqldump -u root -p -d --all-databases > d.sql
```

### 备份数据和结构

(相当于在备份结构的语法上去掉-d选项)

1.备份表结构和数据

```shell
mysqldump -u root -p dbname table1 table2 ... > a.sql
```

2.备份数据库的所有表结构和数据

```shell
mysqldump -u root -p dbname  > b.sql
```

3.备份多个数据库的表结构和数据

```shell
mysqldump -u root -p --databases db1 db2  > c.sql
```

4.备份所有数据库的表结构和数据

```shell
mysqldump -u root -p --all-databases > d.sql
```

* mysqldump -h 127.0.0.1 -u root -p root db_name>path;
  * 使用mysqldump 命令备份数据库
  * -h指定数据库所在的服务器的ip地址
  * -u指定登录数据库的密码
  * db_name是要备份的数据库的名称
  * 使用输出目标操作符>,指定输出的文件具体路径c:/back.sql

### 备份表数据

```sql
mysql -u root -p -e "selec 语句" dbname > 目标文件名

select * from xxx into outfile ‘/tmp/stud.txt' ; 
```



## 命令行还原

### 还原表结构和数据

```shell
mysql -u root -p [dbname] < 目标文件
mysql -h127.0.0.1 -uroot -proot db_name<back.sql

load data infile '/tmp/stud.txt' into table students;
source /backup/all_db_2013-09-08.sql
```



# 高级查询

## distinct

 在`select`语句中，可以使用`distinct`关键字对查询的结果集进行去重。

```sql
select distinct 列1, ... , 列n  from table_name [其他子句];
```

> 去重必须结果集中每个列的值都相同。

## order by

`order by`用于对结果进行排序显示，可以使用`ASC` / `DESC`两种方式进行排序，可以有多个排序条件

- `ASC`：表示升序排序，如果不写即为此排序方式
- `DESC`：表示降序排序

```sql
select [distinct] 列1, ... , 列n from table_name [其他子句] order by 排序列1 [DESC], 排序列2 [DESC];
```

## 分页查询limit子句

```properties
select * from emp limit 0,2;
```

- 第一个参数0是表示从第几条开始查询 (这里的 0 是可以省略不写的)；
- 第二个参数 表示查询出几条数据
- 后面不够的，有多少写多少；

```java 
select * from emp order by empNo limit 5;
select * from emp limit 5,5;

-- 
select * from table_name  limit (页码 - 1) * 每页数量, 每页数量;
```





## 聚合函数

Mysql中内置了 5 种聚合函数，分别是：`SUM` 、`max`、`min`、`avg`、`count`。

- `sum`： 求和

  ```sql
  select sum(列) from table_name [其他子句];
  ```

- `max`: 求最大值

  ```sql
  select max(列) from table_name [其他子句];
  ```

- `min`: 求最小值

  ```sql
  select min(列) from table_name [其他子句];
  ```

- `avg`： 求平均值

  ```sql
  select avg(列) from table_name [其他子句];
  ```

- `count`: 求数量

  ```sql
  select count(列) from table_name [其他子句];
  ```

## group by

`group by ` 是对数据进行分组，分组时，表中有相同值的分为一组。分组后可以进行聚合查询。

`group by`分组后的查询中，`select`的列不能出现除了`group by `分组条件以及聚合函数外的其他列。

```sql
select 列1, 列2, (聚合函数) from table_name group by 列1, 列2;
```

## having

`having`是对`group by`分组后的结果集进行筛选。

```sql
select 列1, 列2, (聚合函数) from table_name group by 列1, 列2 having 分组后条件;
```

## 综合查询

```sql
SELECT DISTINCT emp.deptno FROM emp JOIN dept ON emp.deptno = dept.deptno WHERE bridate >= '2000-01-01' GROUP BY emp.deptno HAVING count(*) >= 2 ORDER BY count(*) DESC  LIMIT 0, 5;
```

> 书写顺序是以上。
>
> `SQL`语句的执行顺序
>
> from --> on --> join --> where --> group by --> having -->  select --> distinct-- > order by--> limit

[sql语句定义和执行顺序](https://blog.csdn.net/u013887008/article/details/93377939)
