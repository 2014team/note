# Mysql

## 基础

### Mysql概述

#### **数据库相关概念**

| 名称      | 说明                              | 简称                               |
| :------ | ------------------------------- | -------------------------------- |
| 数据库     | 存储数据的仓库，数据是有组织的进行存储             | DataBase(DB)                     |
| 数据库管理系统 | 操纵和管理数据库的大型软件                   | DataBase Management System(DBMS) |
| SOL     | 操作关系型数据库的编程语言，定义了一套操作关系型数据库统一标准 | Structured Query Language (SQL)  |

**关系型数据库(RDBMS)**

概念:建立在关系模型基础上，由多张相互连接的二维表组成的数据库。

**特点:**

1. 使用表存储数据，格式统一，便于维护

2. 使用SQL语言操作，标准统一，使用方便


![](image/1718962769662.jpg)

### SQL

**SQL (Structured Query Language)** 是具有数据操纵和数据定义等多种功能的数据库语言，这种语言具有交互性特点，能为用户提供极大的便利，数据库管理系统应充分利用SQL语言提高计算机应用系统的工作质量与效率

#### SQL通用语法

1. SQL语句可以单行或多行书写，以分号结尾。
2. SQL语句可以使用空格/缩进来增强语句的可读性
3. MySOL数据库的SQL语句不区分大小写，关键字建议使用大写。
4. 注释:
   单行注释: --注释内容 或#注释内容(MySQL特有)
   多行注释: /*注释内容 */

#### SQL分类

| 分类   | 全称                         | 说明                          |
| ---- | -------------------------- | --------------------------- |
| DDL  | Data Definition Langugge   | 数据定义语言，用来定义数据库对象(数据库，表，字段)  |
| DML  | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改     |
| DQL  | Data Query Language        | 数据查询语言，用来查询数据库中表的记录         |
| DCL  | Data Control Language      | 数据控制语言，用来创建数据库用户、控制数据库的访问权限 |

#### DDL(Data Definition Language)  数据定义语言

**数据库操作**

**查询**

   查询所有数据库

```
SHOW DATABASES;
```

   查询当前数据库

```
 SELECT DATABASE();
```

**创建**

```
 CREATE DATABASE [IF NOT EXISTS]  数据库名 [DEFAULT CHARSET 字符集] [COLLATE  排序规则];
```

**删除**

```
DROP DATABASE [IF EXISTS] 数据库名;
```

**切换数据库**

```
 USE 数据库名;
```

**表操作-查询**

**查询当前数据库所有表**

```
SHOW TABLES;
```

**查询表结构**

```
  DESC 表名;
```

**查询指定表的创建表语句**

```
SHOW CREATE TABLE 表名;
```

**表操作-创建**

```
CREATE TABLE 表名(
  字段1  字段1类型  [COMMENT 字段1注释]
  字段2  字段2类型  [COMMENT 字段2注释]
  ....
  字段n  字段n类型  [COMMENT 字段n注释]
)[COMMENT 表注释];
```

**表操作-修改**

**添加字段**

```
ALTER TABLE 表名  ADD  字段名称  类型(长度) [COMMENT 注释][约束];
```

**修改数据类型**

```
ALTER TABLE 表名  MODIFY 字段名称 新数据类型(长度)
```

**修改字段名和字段类型**

```
ALTER TABLE 表名  CHANGE  旧字段名  新字段名 类型(长度)[COMMENT 注释][约束];
```

**修改表名**

```
ALTER TABLE 表名 RENAME TO 新表名;
```

**表操作-删除**

**删除字段**

```
ALTER 表名  DROP 字段名称;
```

**删除表**

```
DROP TABLE [IF EXISTS] 表名;
```

**删除指定表，并重新创建表**

```
TRUNCATE TABLE 表名;
```

#### DML(Data Manipulation Language) 数据操作语言

**添加数据**

**给指定字段添加数据**

```
INSERT INTO  表名（字段1,字段2,....）VALUES(值1，值2,....);
```

**给全部字段添加数据**

```
INSERT INTO 表名 VALUES(值1，值2,...);
```

**批量加数据**

```
INSERT INTO  表名 VALUES(值1，值2,....),(值1，值2,....);
```

**修改数据**

```
UPDATE 表名  SET 字段名1=值1, 字段名2=值2,... [WHERE 条件];
```

**删除数据**

```
DELETE FROM 表名 [WHERE 条件];
```

#### DQL(Data Query Language)数据查询语言

**查询语法**

```
SELECT 
   字段列表
FROM 
   表名列表
WHERE
   条件列表
GREOUP BY
   分组字段列表
HAVING
   分组后条件列表
ORDER BY
   排序字段列表
LIMIT
   分页参数
```

 **查询多个字段**

```
 SELECT 字段1，字段2,.... FROM 表名;
 SELCET * FROM 表名;
```

 **设置别名**

```
SELECT 字段1[AS 别名1]，字段2[AS 别名2],.... FROM 表名;
```

 **去除重复记录**

```
 SELECT DISTINCT 字段列表  FROM 表名;
```

 **条件查询**

```
SELECT 字段列表 FROM 表名  WHERE 条件列表;
```

| **比较运算符**      | **功能**                                |
| ------------------- | --------------------------------------- |
| >                   | 大于                                    |
| >=                  | 大于等于                                |
| <                   | 小于                                    |
| <=                  | 小于等于                                |
| =                   | 等于                                    |
| <>或!=              | 不等于                                  |
| BETWEEN .... AND... | 在某个范围之内(含最小值，含最大值)      |
| INT(...)            | 在in之后的列表中的值，多选一            |
| LIKE 占位符         | 模糊匹配( 匹配单个字符,%匹配任意个字符) |
| IS NULL             | 是NULL                                  |
| AND 或 &&           | 并且(多个条件同时成立)                  |
| OR 或 \|\|          | 或者(多个条件任意一个成立)              |
| NOT 或!             | 非，不是                                |

**聚合函数**

将一列数据作为一个整体，进行纵向计算

```
SELECT 聚合参数(字段列表) FROM 表名;
```

| **函数** | **功能** |
| -------- | -------- |
| count    | 统计数量 |
| max      | 最大值   |
| min      | 最小值   |
| avg      | 平均值   |
| sum      | 求和     |

**分组查询**

```
SELECT 字段列表 FROM 表名[WHERE 条件]GROUP BY 分组字段名 [HAVING 分组后过滤条件];
```

where与having区别

执行时机不同:where是分组之前进行过滤，不满足where条件，不参与分组;而having是分组之后对结果进行过滤。

判断条件不同:where不能对聚合函数进行判断，而having可以。

注意:

执行顺序: where >聚合函数>having  

分组之后，查询的字段一般为聚合函数和分组字段，查询其他字段无任何意义

**排序查询**

```
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1,字段2 排序方式2;
```

排序方式

ASC:升序(默认值)

DESC:降序

注意:

如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序

**分页查询**

```
SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数;
```

起始索引从0开始，起始索引=K查询页码-1)*每页显示记录数
分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT

如果查询的是第一页数据，起始索引可以省略，直接简写为limit 10

**查询DQL执行顺序**

![](image\1715565204647.png)

#### **DCL**(Data Control Language) 数据控制语言

| **权限**            | **说明**           |
| ------------------- | ------------------ |
| ALL, ALL PRIVILEGES | 所有权限           |
| SELECT              | 查询权限           |
| INSERT              | 插入权限           |
| UPDATE              | 修改权限           |
| DELETE              | 删除权限           |
| ALTER               | 修改表             |
| DROP                | 删除数据库/表/视图 |
| CREATE              | 创建数据库/表      |

**DCL-管理用户**

**查询用户**

```
USE mysql;
SELECT * FROM user;
```

**创建用户**

```
CREATE USER '用户名'@'主机名' IDENTIFIED  BY '密码';
```

**修改用户密码**

```
ALTER USER '用户名'@'主机名' IDENTIFIED  WITH mysql_native_password BY '新密码';
```

**删除用户**

```
DROP USER '用户名'@'主机名'
```

**DCL-权限控制**

**查询权限**

```
SHOW GRANTS FOR'用户名'@'主机名':
```

**授予权限**

```
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```

**撤销权限**

```
REVOKE 权限列表 ON 数据库名.表名 FROM'用户名'@'主机名';
```

多个权限之间，使用逗号分隔

授权时，数据库名和表名可以使用*进行通配，代表所有

### 数据类型

**数字类型**

**![1715567309066.png](image\1715567309066.png)**

**字符类型**

**![1715567315566.png](image\1715567315566.png)

**日期类型**

![1715567336182.png](image\1715567336182.png)

### 函数

MySQL函数，是一种控制流程函数，属于数据库用语言，包含CASE WHEN THEN 函数、IF 函数、 IFNULL 函数等。

#### 字符串函数

| **函数**                 | **功能**                                                  |
| ------------------------ | --------------------------------------------------------- |
| CONCAT(S1,S2,....Sn)     | 字符串拼接，将S1，S2，….Sn拼接成一个字符串                |
| LOWER(str)               | 将字符串str全部转为小写                                   |
| UPPER(str)               | 将字符串str全部转为大写                                   |
| LPAD(str,n,pad)          | 左填充，用字符串pad对str的左边进行填充，达到n个字符串长度 |
| RPAD(str,n,pad)          | 右填充，用字符串pad对str的右边进行填充，达到n个字符串长度 |
| TRIM(str)                | 去掉字符串头部和尾部的空格                                |
| SUBSTRING(str,start,len) | 返回从字符串str从start位置起的len个长度的字符串           |

**CONCAT**

```
SELECT CONCAT('Hello' 'World');
```

结果： HelloWorld

**LOWER**

```
SELECT LOWER('HELLO')
```

结果： hello

**UPPER**

```
SELECT UPPER('hello')
```

结果： HELLO

**LPAD**

```
SELECT LPAD('1',5,'0')
```

结果： 00001

**RPAD**

```
SELECT RPAD('1',5,'0')
```

结果： 10000

**TRIM**

```
SELECT TRIM(' Hello  World ')
```

结果： Hello World

**SUBSTRING**

```
SELECT SUBSTRING('helloworld',1,5)
```

结果：hello

#### 数值安函数

| **函数**   | **功能**                           |
| ---------- | ---------------------------------- |
| CEIL(x)    | 向上取整                           |
| FLOOR(x)   | 向下取整                           |
| MOD(x,y)   | 返回x/y的模                        |
| RAND()     | 返回0~1内的随机数                  |
| ROUND(x,y) | 求参数x的四舍五入的值，保留y位小数 |

**CEIL**

```
SELECT CEIL(1.9)
```

结果： 2

**FLOOR**

```
SELECT FLOOR(1.9)
```

结果： 1

**MOD**

```
SELECT MOD(5,4)
```

结果： 1

**RAND**

```
SELECT RAND()
```

结果： 0.1341812388358463

**ROUND**

```
SELECT ROUND(3.446,2)
```

结果： 3.45

#### 日期函数

| **函数**                          | **功能**                                          |
| --------------------------------- | ------------------------------------------------- |
| CURDATE()                         | 返回当前日期                                      |
| CURTIME()                         | 返回当前时间                                      |
| NOW()                             | 返回当前日期和时间                                |
| YEAR(date)                        | 获取指定date的年份                                |
| MONTH(date)                       | 获取指定date的月份                                |
| DAY(date)                         | 获取指定date的日期                                |
| DATE ADD(date,INTERVAL expr type) | 返回一个日期/时间值加上一个时间间隔expr后的时间值 |
| DATEDIFF(date1,date2)             | 返回起始时间date1 和 结束时间date2之间的天数      |

**CURDATE**

```
SELECT CURDATE()
```

结果：2024-05-15

**CURTIME**

```
SELECT CURTIME()
```

结果：22:27:18

**NOW**

```
SELECT NOW()
```

结果：2024-05-15 22:27:29

**YEAR**

```
SELECT YEAR(CURDATE())
```

结果：2024

**MONTH**

```
SELECT MONTH(CURDATE())
```

结果：5

**DAY**

```
SELECT DAY(CURDATE())
```

结果：15

**DATE_ADD**

```
SELECT DATE_ADD(CURDATE(),INTERVAL 10 YEAR)
```

结果：2034-05-15

**DATEDIFF**

```
SELECT DATEDIFF(CURDATE(),CURDATE())
```

结果：0

#### 流程函数

| **函数**                                                  | **功能**                                               |
| --------------------------------------------------------- | ------------------------------------------------------ |
| IF(value ,t,f)                                            | 如果value为true，则返回t，否则返回f                    |
| IFNULL(value1 ,value2)                                    | 如果value1不为空，返回value1，否则返回value2           |
| CASE WHEN [val1 ] THEN [res1]... ELSE [default] END       | 如果val1为true，返回res1，…否则返回default默认值       |
| CASE「expr]WHEN [val1 ] THEN [res1] ... ELSE[ default]END | 如果expr的值等于val1，返回res1，…否则返回default默认值 |

 **IF**

```
SELECT IF(TRUE,'ok','no')
```

结果：ok

**IFNULL**

```
SELECT IFNULL(NULL,'ok')
```

结果：ok

**CASE WHEN [val1 ] THEN [res1]... ELSE [DEFAULT] END**

```
SELECT CASE WHEN 1=1 THEN 'true' ELSE 'false' END
```

结果：true

**CASE「expr]WHEN [val1 ] THEN [res1] ... ELSE[ DEFAULT]END**

![1715784476976.png](image\1715784476976.png)

![1715784490449.png](image\1715784490449.png)

### 约束

约束是作用于表中字段上的规则，用于限制存储在表中的数据。

目的：保证数据库中数据的正确、有效性和完整性。

| **约束**                 | **描述**                                                 | **关键字**  |
| ------------------------ | -------------------------------------------------------- | ----------- |
| 非空约束                 | 限制该字段的数据不能为null                               | NOT NULL    |
| 唯一约束                 | 保证该字段的所有数据都是唯一、不重复的                   | UNIQUE      |
| 主键约束                 | 主键是一行数据的唯一标识，要求非空且唯一                 | PRIMARY KEY |
| 默认约束                 | 保存数据时，如果未指定该字段的值，则采用默认值           | DEFAULT     |
| 检查约束(8.0.16版本之后) | 保证字段值满足某一个条件                                 | CHECK       |
| 外键约束                 | 用来让两张表的数据之间建立连接，保证数据的一致性和完整性 | FOREIGN KEY |

**示例**

**![1716987548688.png](image\1716987548688.png)**

```sql
create table user(
id int primary key auto_increment comment '主键',
name varchar(10) not null unique comment '姓名',
age int check(age>0 && age<= 120)comment '年龄',
status char(1) default '1' comment '状态',
gender char(1) comment '性别'
)comment '用户表'
```

**外键约束语法**

**创建表操作**

```
CREATE TABLE 表名(
字段名 数据类型,
....
[CONSTRAINT][外键名称]FOREIGN KEY(外键字段名)REFERENCES 主表(主表列名)
);
```

**创建表之后创建约束**

```
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY(外键字段名)REFERENCES 主表(主表列名):
```

**删除外键**

```
ALTER TABLE 表备 DROP FOREIGN KEY 外键名称;
```

 **删除/更新行为**

| 行为        | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| NO ACTION   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。(与RESTRICT 一致) |
| RESTRICT    | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。(与NO ACTION一致) |
| CASCADE     | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录。 |
| SET NULL    | 当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为nul(这就要求该外键允许取null)。 |
| SET DEFAULT | 父表有变更时，子表将外键列设置成一个默认的值(Innodb不支持)   |

语法

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGNKEY(外键字段)REFERENCES 主表名(主表字段名)ON UPDATE CASCADE ON DELETE CASCADE;
```

### 多表查询

#### 一对一

示例：用户基本信息表中的用户对应用户教育表中的一条数据。

![1718802752895.png](image\1718802752895.png)

#### 一对多

多个员工在一个部门

![1718802877043.png](image\1718802877043.png)

#### 多对多

学生可以选择多门课程，课程也可以被多个学生选择。

多对多一般需要借助第三张表做关联关系。

![1718802965965.png](image\1718802965965.png)

![1718802627335.png](image\1718802627335.png)

![1718803262886.png](image\1718803262886.png)

#### 查询语法

![1718803381220.png](image\1718803381220.png)

![1718803478583.png](image\1718803478583.png)

![1718803489006.png](image\1718803489006.png)

![1718803672552.png](image\1718803672552.png)

![1718803504914.png](image\1718803504914.png)

![1718803528175.png](image\1718803528175.png)![1718803551607.png](image\1718803551607.png)

![1718803569658.png](image\1718803569658.png)

**多表关系**

**一对多**:在多的一方设置外键，关联一的一方的主键

**多对多**:建立中间表，中间表包含两个外键，关联两张表的主键

**一对一**:用于表结构拆分，在其中任何一方设置外键(UNIOUE)，关联另一方的主键



**多表查询**

**内连接**

**隐式**SELECT... FROM 表A,表B WHERE 条件.

**显式**SELECT.. FROM 表A INNER JOIN 表B ON 条件.

**外连接**

**左外** SELECT.. FROM 表A LEFT JOIN 表B ON 条件

**右外**SELECT.. FROM 表A RIGHT JOIN 表B ON 条件

**自连接**:SELECT.. FROM 表A 别名1,表A 别名2 WHERE 条件

**子查询**:标量子查询、列子查询、行子查询、表子查询

### 事务

**事务** 是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失败。

示例：张三给李四转账，转账操作要么成功要么失败，不能张三账号扣除金额了，而李四账号确没有收到张三转账的金额。

第一步，开启事务

第二步，查询账号账户是否有充足的余额。

第三步，账号账户扣除需要转账的金额。

第四步，李四账号加上张三转账的金额。

第五步，提交事务

说明：要是在事务中有异常，需要回滚事务。

![1718865215810.png](image\1718865215810.png)

#### 事务操作

![1718865951482.png](image\1718865951482.png)

说明：默认MySQL的事务是自动提交的，也就是说，当执行一条DML语句，MySQL会立即隐式的提交事务。

#### 四大特性

**原子性**(Atomicity):事务是不可分割的最小操作单元，要么全部成功，要么全部失败。

**一致性**(Consistency):事务完成时，必须使所有的数据都保持一致状态。

**隔离性**(lsolation):数据库系统提供的隔离机制，保证事务在不受外部并发操作影响的独立环境下运行。

**持久性**(Durability):事务一旦提交或回滚，它对数据库中的数据的改变就是永久的。

#### 隔离级别

![1718866182299.png](image\1718866182299.png)

查看全局隔离级别

```
SELECT @@global.tx_isolation;
```

查看当前会话的隔离级别

```
SELECT @@session.tx_isolation;
```



设置当前会话的隔离级别：

```
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

设置全局隔离级别：

```
SET GLOBAL TRANSACTION ISOLATION LEVEL READ COMMITTED;
```



设置事务隔离语法

```
SET [SESSION GLOBAL] TRANSACTION ISOLATION LEVEL { READ UNCOMMITTED | READ COMIMITTED | REPEATABLE READ | SERIALIZABLE }
```



```
SELECT @@autocommit;  -- 1事务自动提交  0事务手动提交
SET @@autocommit= 1; -- 设置事务隔离级别
```

**MySQL** 默认事务隔离级别：REPEATABLE READ

**Oracle** 默认事务隔离级别：READ COMMITTED

**SQL Server** 默认事务隔离级别：READ COMMITTED

#### 并发问题

![1718866239705.png](image\1718866239705.png)

说明：需要验证事务并发问题可以开启两个操作数据库的客户端开启各自事务测试。

## 进阶

### 存储引擎

存储引擎是数据库管理系统 (DBMS) 中的一种组件，负责管理数据库的物理存储、数据的读写操作以及相关的存储管理。不同的存储引擎在数据处理、性能优化和功能支持上有所不同，因此可以根据具体应用需求选择合适的存储引擎

#### **存储引擎作用**

- **数据存储**：定义如何将数据物理存储在磁盘上，包括数据文件的格式和存储位置。
- **数据读写**：处理对数据库的读写操作，包括插入、更新、删除和查询等。
- **事务处理**：支持或不支持事务处理（事务是一组数据库操作的集合，要么全部执行，要么全部不执行），例如 InnoDB 支持事务而 MyISAM 不支持。
- **锁机制**：管理并发访问时的数据锁定机制，以防止数据不一致或竞争条件。行级锁定和表级锁定是两种常见的锁机制。
- **索引管理**：支持创建和管理索引以加速查询操作，不同存储引擎支持不同类型的索引。
- **数据完整性**：保证数据的准确性和一致性，包括支持外键约束等。
- **崩溃恢复**：提供数据恢复机制，以在系统崩溃后恢复数据。

#### 存储引擎

1. **InnoDB**：默认存储引擎，支持事务、行级锁定和外键约束，适合高并发和需要数据完整性的应用。在 MySQL 5.5之后，InnoDB是默认的 MySQL 存储引擎。
2. **MyISAM**：不支持事务和外键，表级锁定，适合读密集型操作。
3. **MEMORY**：数据存储在内存中，速度快，但不适合持久存储，适用于临时数据。
4. **CSV**：数据存储在 CSV 文件中，便于数据交换，但不支持索引和复杂查询。
5. **ARCHIVE**：用于存储大量的历史数据，压缩存储，适合需要较小存储空间的日志数据。
6. **NDB (Cluster)**：用于 MySQL Cluster，支持高可用性和高可扩展性。
7. **FEDERATED**：允许访问远程 MySQL 服务器上的表，适合分布式数据库系统。

#### **体系结构**

![1719147539457.png](image\1719147539457.png)

最上层是一些客户端和链接服务，主要完成一些类似于连接处理、授权认证、及相关的安全方案。服务器也会为安全接入的每个客户端验证它所具有的操作权限。

**服务层**

第二层架构主要完成大多数的核心服务功能，如SQL接口，并完成缓存的查询，SQL的分析和优化，部分内置函数的执行。所有跨存储引擎的功能也在这一层实现，如过程、函数等。

**引擎层**

存储引擎真正的负责了MySOL中数据的存储和提取，服务器通过API和存储引擎进行通信。不同的存储引擎具有不同的功能，这样我们可以根据自己的需要，来选取合适的存储引擎。

**存储层**

主要是将数据存储在文件系统之上，并完成与存储引擎的交互。

在创建表时，指定存储引擎

```sql
CREATE TABLE 表名(
字段1字段1类型「COMMENT 字段1注释]
字段n 字段n类型[COMMENT 字段n注释])ENGINE=INNODB[COMMENT 表注释];
```

查看当前数据库支持的存储引擎

```sql
SHOW ENGINES ;
```

#### 存储引擎比较

| **特点**     | **InnoDB**        | **MyISAM** | **Memory** |
| ------------ | ----------------- | ---------- | ---------- |
| 存储限制     | 64TB              | 有         | 有         |
| 事务安全     | **支持**          | -          | -          |
| 锁机制       | **行锁**          | 表锁       | 表锁       |
| B+tree索引   | 支持              | 支持       | 支持       |
| Hash 索引    | -                 | -          | 支持       |
| 全文索引     | 支持（5.6版本后） | 支持       | -          |
| 空间使用     | 高                | 低         | N/A        |
| 内存使用     | 高                | 低         | 高         |
| 批量插入速度 | 低                | 高         | 高         |
| 支持外键     | **支持**          | -          | -          |

#### InnoDB 表空间文件说明

InnoDB 支持两种表空间管理模式：共享表空间 (Shared Tablespace) 和 独立表空间 (File-Per-Table Tablespace)。默认情况下，从 MySQL 5.6 版本开始，InnoDB 使用的是独立表空间模式。



**共享表空间 (Shared Tablespace)**

- 在共享表空间模式下，所有 InnoDB 表的数据和索引都存储在一个或多个共享表空间文件中。默认的共享表空间文件名为 ibdata1。这个文件通常位于 MySQL 数据目录下。

  **特点**：

- 所有表的数据和索引都存储在同一个或多个共享文件中。

- 管理简单，不需要为每个表单独管理文件。

- 随着数据量的增加，文件会变得很大，难以单独管理某个表的数据。

- 删除表后，空间不能立即回收。

**独立表空间 (File-Per-Table Tablespace)**

- 在独立表空间模式下，每个 InnoDB 表的数据和索引存储在一个独立的 .ibd 文件中。这个文件存储在对应数据库目录下。

  **特点**：

- 每个表的数据和索引存储在独立的 .ibd 文件中。

- 便于管理单个表的数据和空间，可以单独转移或备份表的数据文件。

- 删除表后，对应的 .ibd 文件也会被删除，从而回收磁盘空间。

- 文件数量增多，文件系统管理较为复杂。

**配置独立表空间**

独立表空间是 MySQL 5.6 及更高版本的默认设置。可以通过以下方式检查和设置独立表空间的使用情况：



**查看当前设置**：

```sql
SHOW VARIABLES LIKE 'innodb_file_per_table';
```

**启用独立表空间**：

```sql
SET GLOBAL innodb_file_per_table = 1;
```

**在 MySQL 配置文件 `my.cnf` 中设置**：

```sql
[mysqld]
innodb_file_per_table=1
```

**禁用独立表空间**（切换回共享表空间模式）：

```sql
SET GLOBAL innodb_file_per_table = 0;
```

#### InnoDB 逻辑存储结构

![1719152462207.png](image\1719152462207.png)

**共享表空间 (Shared Tablespace)：**

默认情况下，所有 InnoDB 表的数据和索引都存储在一个或多个共享的表空间文件中。这些文件通常命名为 ibdata1、ibdata2 等，位于 MySQL 的数据目录中。

共享表空间包含了数据字典、数据和索引等的基本结构，是 InnoDB 存储引擎的核心。



**独立表空间 (File-Per-Table Tablespace)：**

在启用独立表空间模式时，每个 InnoDB 表都会有一个独立的 .ibd 文件，该文件包含该表的数据和索引。

独立表空间模式更灵活，允许单独管理每个表的数据文件，进行单表备份和恢复，以及更精确地控制存储空间的使用。



**段 (Segments)**

InnoDB 将数据和索引组织成段 (Segments)。每个段由一个或多个连续的数据页组成。主要的段类型包括数据段、索引段和回滚段等。每个表都有自己的数据段和至少一个索引段。

数据段 (Data Segment)：存储表的数据。

索引段 (Index Segment)：存储表的索引。

回滚段 (Rollback Segment)：用于支持事务的回滚操作。



**区 (Areas)**

在 InnoDB 存储引擎中，数据和索引管理是基于不同的区域 (Areas) 进行的。每个区域负责管理特定类型的数据页或数据段。主要的区域包括：

缓冲池 (Buffer Pool)：用于缓存常用的数据和索引页，提高查询性能。

日志缓冲 (Log Buffer)：用于存储事务提交前的修改操作，以提高事务处理速度。

重做日志文件组 (Redo Log Files Group)：记录每个事务的操作，用于在数据库崩溃时进行恢复。



**页 (Pages)**

InnoDB 将数据和索引组织成固定大小的数据页，默认大小为 16KB（可以通过配置进行修改）。每个数据页是 InnoDB 存储引擎的基本存储单元。InnoDB 的数据和索引都存储在这些页中，而不是像 MyISAM 引擎那样存储在固定大小的块中。



InnoDB 存储引擎通过逻辑存储结构（表空间、页、段和区）有效地管理数据和索引。这种结构提供了高效的数据访问、事务管理和崩溃恢复能力，使得 InnoDB 成为广泛使用的关系型数据库管理系统的首选存储引擎之一。