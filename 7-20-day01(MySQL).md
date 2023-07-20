# MYSQL

### 常见的数据库：

Oracle ：收费的大型数据库， Oracle 公司的产品。

MYSQL ： 开 源 免 费 、 中 小 型 的 数 据 库 。 2009 年Oracle 收购 SUN 公司，从 MYSQL6.x 版本开始收费，但是还有免费的社区版本。

SQLServer ： MicroSoft 公司收费的中型的数据库。C# 、 .net 等语言常使用。

PostgreSQL ：开源免费的中小型数据库，能被苹果公司大量使用并替换早期的 MySQL 数据库，说明其一定 有 不 俗 的 表 现 。 在 2023 年 的 数 据 库 排 行 榜 上 ，

PostgreSQL 位居第四位，号称世界上最先进的、最安全的开源数据库。

DB2 ： IBM 公司的数据库产品,收费的。常应用在银行系统中

SQLite : 嵌入式的小型数据库，应用在手机端。

### 常用数据库：

 MYSQL ， Oracle 。 在web应用中，使用的最多的就是MySQL 数据库，原因如下：

	1. 开源、免费
	2. 功能足够强大，足以应付web应用开发

- 关系型数据库都是使用SQL语言来进行统一操作，SQL语言是操作关系型数据库的 统一标准。

`select version(); # 查询MySQL版本`

```mysql
# 在bin目录下执行
  mysql -u root -p # MYSQL内置一个 用户账号为root， 密码为空
3
4 select version(); # 查询MySQL版本
5
6 # 解决root无密码登录不了的问题
7 # 以不检查权限的方式启动 先停止mysql服务
8 safe_MySQLd - skip -grant -tables
9 update MySQL.user set password=PASSWORD('新密码') where User ='root'
10 flush privileges；1
11
12
13
14 # 解决端口冲突问题
15 netstat -ano|findstr 3306 # 查询正在执行3306端口的程序，如果有 在任务栏找到对应程序结束任务就可以了
16 # 退出数据库,exit / quit 都可以退出数据库
17 exit
18 quit
```



> mysql [-h 127.0.0.1] [-P 3306] -u root -p

- 参数：

  - -h : MySQL服务所在的主机IP

  - -P : MySQL服务端口号， 默认3306

  - -u : MySQL数据库用户名

  - -p ：MySQL数据库用户名对应的密码

### 关系型数据库

概念：建立在关系模型基础上，由多张相互连接的二维表组成的数据库

1. 使用表存储数据，格式统一，便于维护

2. 使用SQL语言操作，标准统一，使用方便数据模型

客户端连接数据库管理系统，数据库管理系统中有多个数据库，数据库中都有多张表

### **SQL**通用语法

1. 单行或者多行书写，以分号结束

2. 可以使用空格或者缩进来增强语句的可读性

3. mysql数据库中，SQL语句不区分大小写，关键字建议使用大写

### 注释

- 单行注释 # --

- 多行注释， /* */

### 分类

1. **DDL** 数据定义语言，用来定义数据库对象（数据库，表，字段）

2. **DML** 数据操作语言，用来对数据表中的数据进行增删改

3. **DQL** 数据查询语言，用来查询数据库中表的记录

4. **DCL** 数据控制语言，用来创建数据库用户，控制数据库的访问权限DDL 语句

### 数据库

1. 查看数据库

2. 创建新数据库

3. 选择数据库

4. 删除数据库

- `show databases`; # 查看当前用户可操作的所有数据库

- `CREATE DATABASE [IF NOT EXISTS]` 数据库名字 [DEFAULT CHARSET utf8mb4];

> 数据库中，命名一般是使用`_`连接多个单词;
>
> 数据库中 SQL 语句执行失败后会有错误提示，错误提示包括错误信息和错误编号。我们可以直接拿错误编号去搜索。
>
> 有时在创建数据库时要设置数据库的编码。`MySQL 8`默认编码为`UTF-8`，满足我们需求所以不需要设置。如果使用的是低版本数据库则需要在创建数据库时加上`CHARACTER SET utf8`去设置编码。或者使用`ALTER DATABASE db_name CHARACTER SET UTF8;`修改

\# mysql8 中创建的数据库默认编码是'utf8mb4'

`use 数据库名;`

\# 选择数据库之后可以在其中创建数据库表

- `select database();`

- `drop database 数据库名;`

### **DDL--** 表管理

- 查看表

数据表中包含若干列，每列需要明确列中存储的数据类型，如字符串、日期时间、证书、浮点数等等。

```mysql
show tables;
# 查看当前被选中的数据库中的所有表
```

- 创建表

```mysql 
CREATE TABLE [IF NOT EXISTS] tab_name(

	col_name datatype [COMMENT '注释'],

	col_name datatype

)[CHARACTER set 编码格式];
```

* 使用CREATE TABLE table关键词创建数据表
* tab_name是数据表的名称
* col_name是列名称
* datatype是列的数据类型
* DEFAULT 是默认值
* COMMENT 是注释

```mysql
  CREATE TABLE dept(
  deptno INT DEFAULT 1 COMMENT '部门编号',
  deptname VARCHAR(20) DEFAULT NULL COMMENT '部门名称'
  )CHARACTER SET utf8;

  -- 显示所有表
  SHOW tables;
```

查看表结构

```mysql
describe 表名;

desc 表名;

show create table 表名;
```

- 删除表

  ```mysql
  drop table 表名;
  ```

### 用户管理

1. 查看当前登录的用户

```mysql
select user() [from dual]; # 查看当前登录的用户
```

dual 虚拟表，为了让select语句完整

2. 创建新用户

```mysql
create user 用户名@'ip主机地址192.168.31.34' identified by '密码';
```

3. 修改密码

```mysql
alter user 用户名@'ip主机地址'identified by '密码' password expire never;
# 修改密码之后不需要重新登录
```

4. 查询用户信息

```mysql
select user,host from mysql.user;
```

5. 用新用户登录

```mysql
mysql -u 用户名 [-h ip地址] -p
# 新创建的用户只有登录权限，需要使用管理员账户授权
```

6. 为用户授权

```mysql
show grants for 用户名@localhost; #查询用户的权限
2
3 数据库名 . 表名 *.* 数据库名.*
4 grant all on kfm.carts to txsy@localhost;
5 # all 代表所有权限
6
7 # 授权的新用户需要重新登录才能使用新权限
8
9 # 任意ip可以访问
10 GRANT ALL PRIVILEGES ON *.* TO '用户名'@'%';
11 update mysql.user set host='%' where user='txsy;
12
13
14 flush privileges;
```

`all` ：所有权限

`select `：查询权限

`insert` ：插入权限

`update` ：更新权限

7. 删除用户

```mysql
 drop user 用户名@'localhost';
```


​    