# 安装MySQL



1. 解压`mysql-8.0.30-winx64.zip`到 `d:/kaifamiao/envirments`文件夹下

2. 输入`cmd`使用管理员方式打开命令提示窗口

3. 使用命令将目录调整到`D:\kaifamiao\enviroments\mysql-8.0.30-winx64`目录下

   - `cd` 
   - `盘符:`
   - `dir`
   - `../`
   - `./`

4. 依次执行脚本

   1. `1initialization.bat` 初始化。完成后会有一个`data`目录产生
   2. `2install.bat` 安装 `mysql` 服务
      1. 看到`Service successfully installed.`表示服务安装成功

   3. `3startup.bat` 启动`mysql ` 服务
      1. MySQL 服务正在启动 .
         MySQL 服务已经启动成功。
   
   
   > `4reboot.bat`为重启服务命令
   >
   > `5stop.bat`为停止服务命令
   >
   > `6uninstall.bat` 为卸载服务命令
   
   **注意：**初始化脚本只需要执行一次。如果在某个过程出错，删掉目录，重新来过即可。



## 验证安装

前提：启动了`mysql`服务后, 进入到 `{mysql根目录}/bin`

1. `cmd`窗口中输入以下命令：

   ```shell
   mysql -u root -p
   ```

2. 能够进入到`mysql`即为成功安装。

> 如果出现以下内容：
>
> 1. 'mysql' 不是内部或外部命令，也不是可运行的程序或批处理文件。
>    1. 检查是否是在 `bin`目录下执行的此命令

那么为什么一定要在`bin`文件夹下才能进入到 `mysql`目录呢？

- 输入`mysql`命令实际上是要执行`mysql.exe`这个程序在`bin`文件夹中

那么我们可以在其他地方使用 `mysql`命令嘛？

- 当然可以。但是需要我们配置环境变量
- 修改环境变量`path`的值，添加`D:\kaifamiao\enviroments\mysql-8.0.30-winx64\bin`

# MYSQL

# 数据库

## 什么是数据库

​	数据库是以一定方式储存在一起、能与多个用户共享、具有尽可能小的冗余度、与应用程序彼此独立的数据集合，可视为电子化的文件柜——存储电子文件的处所，用户可以对文件中的数据进行新增、查询、更新、删除等操作。

## 数据的存储方式

1. 数据保存在内存
   例如:数组,集合;new出来的对象存储在堆中.堆是内存中的一小块空间
   优点：内存速度快 缺点：断电/程序退出,数据就清除了.内存价格贵
2. 数据保存在普通文件 优点：永久保存 缺点：查找，增加，修改，删除数据比较麻烦，效率低
3. 数据保存在数据库 优点：永久保存,通过`SQL`语句比较方便的操作数据库

## 数据库的优点

数据库是按照特定的格式将数据存储在文件中，通过`SQL`语句可以方便的对大量数据进行增、删、改、查操作，数据库是对大量的信息进行管理的高效的解决方案。

## 数据库管理系统

数据库管理系统（DataBase Management System，DBMS）：指一种操作和管理数据库的大型软件，用于建立、使用和维护数据库，对数据库进行统一管理和控制，以保证数据库的安全性和完整性。用户通过数据库管理系统访问数据库中表内的数据

## 数据库管理系统、数据库和表的关系

数据库管理程序(DBMS)可以管理多个数据库，一般开发人员会针对每一个应用创建一个数据库。为保存应用中实体的数据，一般会在数据库创建多个表，以保存程序中实体的数据。数据库管理系统、数据库和表的关系如图所示：

![](E:\work\notes\19.mysql\img\dbms.png)

先有数据库 → 再有表 → 再有数据 一个库包含多个表

## 常见数据库

![](E:\work\notes\19.mysql\img\DB.png)

`MYSQL`：开源免费的数据库，小型的数据库。已经被`Oracle`收购了`MySQL6.x`版本也开始收费。 

`Oracle`：收费的大型数据库，`Oracle`公司的产品。`Oracle`收购`SUN`公司，收购`MYSQL`。 

`DB2` ：`IBM`公司的数据库产品,收费的。常应用在银行系统中

`SQLServer`：`MicroSoft` 公司收费的中型的数据库。`C#`、`.net`等语言常使用。

 `SyBase`：已经淡出历史舞台。提供了一个非常专业数据建模的工具`PowerDesigner`。 

`SQLite`: 嵌入式的小型数据库，应用在手机端。
常用数据库：`MYSQL`，`Oracle` 在web应用中，使用的最多的就是`MySQL`数据库，原因如下：

1. 开源、免费

2. 功能足够强大，足以应付web应用开发

   

# 将mysql添加到环境变量

> 将`mysql`的`bin`目录地址添加到`系统环境变量`-->`PATH`中

# 将`mysql`添加到服务

以管理员的方式启动`cmd`(命令提示窗口)，使用命令进入到`[mysql]\bin`，执行如下命令。

> mysqld --install (服务名)
>
> 如:
>
> mysqld --install Mysql 5.7

删除服务命令是:

> mysqld --remove 服务名

# mysql端口被占用解决

在`cmd`窗口下执行如下命令：

> netstat -ano|findstr 3306

- 查找正在执行的`3306`端口程序

如果出现如图所示列表表示以上程序使用了3306端口，找到程序的`PID`(最后一列)

去任务管理栏找到对应程序结束任务就行了。



### 连接MySQL

```shell
mysql -u 用户名 -p 
```

- `mysql --help`查询所有参数

# SQL 分类

- **DDL**: 数据定义语句。 如： CREATE / ALTER / DROP
- **DML:** 数据操纵语句。如：INSERT / UPDATE / DELETE 
- **DQL**: 数据查询语句。如：SELECT 

> 所有的SQL都应该以英文状态下的分号结束`;`

# 建库 建表

**数据库语句的关键词建议最好大写**

* 创建数据库语法结构：

  * CREATE DATABASE [ IF NOT EXISTS ] db_name 

  * CREATE DATABASE 表示创建数据库，是SQL中的关键词

  * db_name是要创建的数据库名称

    ```mysql
    CREATE DATABASE company_info;
    ```

    > 数据库中，命名一般是使用`_`连接多个单词;
    >
    > 数据库中 SQL 语句执行失败后会有错误提示，错误提示包括错误信息和错误编号。我们可以直接拿错误编号去搜索。
    >
    > 有时在创建数据库时要设置数据库的编码。`MySQL 8`默认编码为`UTF-8`，满足我们需求所以不需要设置。如果使用的是低版本数据库则需要在创建数据库时加上`CHARACTER SET utf8`去设置编码。或者使用`ALTER DATABASE db_name CHARACTER SET UTF8;`修改

* 使用数据库：

  * USE db_name

  * 使用USE关键词来指定要使用的数据库

    ```mysql
    USE company_info;
    ```

* 删除数据库语法结构

  * drop database db_name

  * 使用DROP关键字删除数据库

    ```mysql
    DROP DATABASE company_info;
    ```

* 显示所有的数据库

  ```shell
  SHOW DATABASES;
  ```

  

# 创建数据表

* 创建数据表的语法结构

  * CREATE TABLE tab_name(

    col_name datatype default null/number comment '注释',

    col_name datatype

    ) [CHARACTER set 编码格式];

    * 使用CREATE TABLE table关键词创建数据表

    * tab_name是数据表的名称

    * col_name是列名称

    * datatype是列的数据类型

    * DEFAULT 是默认值

    * COMMENT 是注释


~~~mysql
```mysql
  CREATE TABLE dept(
  deptno INT DEFAULT 1 COMMENT '部门编号',
  deptname VARCHAR(20) DEFAULT NULL COMMENT '部门名称'
  )CHARACTER SET utf8;

  -- 显示所有表
  SHOW tables;
```
~~~


​    