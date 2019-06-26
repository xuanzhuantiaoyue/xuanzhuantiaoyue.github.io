---
layout: post
title:  "整理一套sql语言的理解"
categories: 数据库
tags: 数据库
author: 赵醒醒
---

* content
{:toc}

## SQL简介
SQL（结构化查询语言）是用于访问和操作数据库中的数据的标准数据库编程语言。 

SQL是关系数据库系统的标准语言。所有关系数据库管理系统(RDMS)，如MySQL、MS Access、Oracle、Sybase、Informix、

Postgres和SQL Server都使用SQL作为它们的标准数据库语言。




 
## RDBMS
RDBMS 指关系型数据库管理系统，全称 Relational Database Management System。

RDBMS 是 SQL 的基础，同样也是所有现代数据库系统的基础，比如 MS SQL Server、IBM DB2、Oracle、MySQL 以及 Microsoft Access。

RDBMS 中的数据存储在被称为表的数据库对象中。

表是相关的数据项的集合，它由列和行组成。

列是表中的垂直实体，其包含与表中的特定字段相关联的所有信息。

## SQL标准命令
与关系数据库交互的标准SQL命令是创建、选择、插入、更新、删除和删除，简单分为以下几组：

**DDL（数据定义语言）**
数据定义语言用于改变数据库结构，包括创建、更改和删除数据库对象。

用于操纵表结构的数据定义语言命令有：
CREATE TABLE-- 创建（在数据库中创建新表、表视图或其他对象）
ALTER TABLE-- 更改 （修改现有的数据库对象，如表）
DROP TABLE-- 删除  （删除数据库中的整个表、表或其他对象的视图）

**DML（数据操纵语言）**
数据操纵语言用于检索、插入和修改数据，数据操纵语言是最常见的SQL命令。

数据操纵语言命令包括：
INSERT-- 插入 （创建记录）
DELETE-- 删除 （删除记录）
UPDATE-- 修改（修改记录）
SELECT -- 检索 （从一个或多个表检索某些记录） （又称为**DQL数据查询语言**）

**DCL（数据控制语言）**
数据控制语言为用户提供权限控制命令。

用于权限控制的命令有：
GRANT-- 授予权限 
REVOKE-- 撤销已授予的权限 

## SQL 语法规则
SQL语句总是以关键字开始，如SELECT、INSERT、UPDATE、DELETE、DROP、CREATE。
SQL语句以分号结尾。
SQL不区分大小写，意味着update与UPDATE相同。

## 一些最重要的 SQL 命令
SELECT - 从数据库中提取数据
UPDATE - 更新数据库中的数据
DELETE - 从数据库中删除数据
INSERT INTO - 向数据库中插入新数据
CREATE DATABASE - 创建新数据库
ALTER DATABASE - 修改数据库
CREATE TABLE - 创建新表
ALTER TABLE - 变更（改变）数据库表
DROP TABLE - 删除表
CREATE INDEX - 创建索引（搜索键）
DROP INDEX - 删除索引

## SQL SELECT 语法
SELECT 语法用于从数据库中选择数据。  
返回的数据存储在结果表中，称为结果集。 
基本语法：SELECT和FROM
在任何SQL查询语句中都：SELECT和FROM他们必须按顺序排列。SELECT指示要查看哪些列，FROM标识它们所在的表。

SQL SELECT 语法如下所示： 

```
SELECT a,b FROM table;
SELECT * FROM table;
```

## SQL SELECT DISTINCT 语法
SELECT DISTINCT语法用于仅返回不同的（different）值。
在一张表内，一列通常包含许多重复的值; 有时你只想列出不同的（different）值。
SELECT DISTINCT语句用于仅返回不同的（different）值。

SQL SELECT DISTINCT语法如下所示：

```
SELECT DISTINCT a,b FROM table;
```

## SQL WHERE 子句
WHERE 子句用于过滤记录。
WHERE 子句用于提取满足指定标准的记录。 

SQL WHERE 语法

```
SELECT a,b FROM table WHERE condition;
UPDATE table SET a =1  WHERE condition;
DELETE FROM table WHERE condition;
```
## SQL AND & OR 运算符
AND&OR运算符用于根据一个以上的条件过滤记录，即用于组合多个条件以缩小SQL语句中的数据。
WHERE子句可以与AND，OR和NOT运算符结合使用。
AND和OR运算符用于根据多个条件筛选记录：
如果由AND分隔的所有条件为TRUE，则AND运算符显示记录。
如果使用AND运算符组合N个条件。对于SQL语句执行的操作(无论是事务还是查询)，所有由AND分隔的条件都必须为TRUE。 
如果由OR分隔的任何条件为真，则OR运算符显示记录。
如果使用OR运算符组合N个条件。对于SQL语句执行的操作(无论是事务还是查询)，OR分隔的任何一个条件都必须为TRUE。 
如果条件不为TRUE，则NOT运算符显示记录。 

```
SELECT a, b FROM table WHERE condition AND condition AND condition;
SELECT a, b FROM table WHERE condition OR condition OR condition;
SELECT a, b FROM table WHERE NOT condition;
```

## SQL ORDER BY 关键字
ORDER BY 关键字用于按升序或降序对结果集进行排序。
ORDER BY 关键字默认情况下按升序排序记录。
如果需要按降序对记录进行排序，可以使用DESC关键字。

SQL ORDER BY 语法

```
SELECT a, b FROM table ORDER BY a, b ASC|DESC;
SELECT a, b FROM table ORDER BY a ASC , b DESC;
```
## SQL INSERT INTO 语句
INSERT INTO 语句用于向表中插入新的数据行。
SQL INSERT INTO 语法
INSERT INTO 语句可以用两种形式编写。 
第一个表单没有指定要插入数据的列的名称，只提供要插入的值，即可添加一行新的数据：

```
INSERT INTO table(a, b, c) VALUES (a, b, c);
```

第二种，如果要为表中的所有列添加值，则不需要在SQL查询中指定列名称。但是，请确保值的顺序与表中的列顺序相同。INSERT INTO语法如下所示：

```
INSERT INTO table VALUES (a,b,c,...);
```

## 什么是SQL NULL值？
SQL 中，NULL 用于表示缺失的值。数据表中的 NULL 值表示该值所处的字段为空。
具有NULL值的字段是没有值的字段。
如果表中的字段是可选的，则可以插入新记录或更新记录而不向该字段添加值。然后，该字段将被保存为NULL值。
值为 NULL 的字段没有值。尤其要明白的是，NULL 值与 0 或者包含空白（spaces）的字段是不同的。

IS NULL语法

```
SELECT a FROM table WHERE a IS NULL;
```
IS NOT NULL语法

```
SELECT a FROM table WHERE a IS NOT NULL;
```

## SQL UPDATE 语句
UPDATE 语句用于更新表中已存在的记录。

还可以使用AND或OR运算符组合多个条件。                
SQL UPDATE 语法
具有WHERE子句的UPDATE查询的基本语法如下所示： 

```
UPDATE table SET a = value1, b = value2, ... WHERE condition;
```

## SQL DELETE 语句
DELETE语句用于删除表中现有记录。

SQL DELETE 语法

```
DELETE FROM table WHERE condition;
```

## SQL 运算符
**SQL算术运算符**
假设变量 a 的值是：10，变量 b 的值是：20，以下为各运算符执行结果：
|运算符|描述 | 例子|
|-|-|-|
|+|加法，执行加法运算。|例子（a + b 得到 30）|
|-|减法，执行减法运算。|例子（a - b 得到  -10)|
|*|乘法，执行乘法运算。|例子（a * b 得到  200)|
|/|用左操作数除右操作数。|例子（b / a 得到  2)|
|%|用左操作数除右操作数并返回余数。 |例子（b % a 得到 0)|

**SQL比较运算符**
假设变量 a 的值是：10，变量 b 的值是：20，以下为各运算符执行结果：
|运算符|描述|例子|
|--|--|--|
|=|检查两个操作数的值是否相等，如果是，则条件为真(true)。|(a = b) is false.|
|!=|检查两个操作数的值是否相等，如果值不相等则条件为真(true)。|(a != b)  is  true.|
|<>|检查两个操作数的值是否相等，如果值不相等则条件为真(true)。|(a <> b) is true.|
|>|检查左操作数的值是否大于右操作数的值，如果是，则条件为真(true)。|(a > b) is false.|
|<|检查左操作数的值是否小于右操作数的值，如果是，则条件为真(true)。|(a < b) is true.|
|>=|检查左操作数的值是否大于或等于右操作数的值，如果是，则条件为真(true)。|(a >= b) is false.|
|<=|检查左操作数的值是否小于或等于右操作数的值，如果是，则条件为真(true)。|(a <= b) is true.|
|!<|检查左操作数的值是否不小于右操作数的值，如果是，则条件变为真(true)。|(a !< b) is false.|
|!>|检查左操作数的值是否不大于右操作数的值，如果是，则条件变为真(true)。|(a !> b) is true.|

**SQL逻辑运算符**
|运算符| 描述 |
|--|--|
| ALL|ALL运算符用于将值与另一个值集中的所有值进行比较。|
| AND|AND运算符允许在SQL语句的WHERE子句中指定多个条件。 |
| ANY|ANY运算符用于根据条件将值与列表中的任何适用值进行比较。|
| BETWEEN|BETWEEN运算符用于搜索在给定最小值和最大值内的值。| 
| EXISTS|EXISTS运算符用于搜索指定表中是否存在满足特定条件的行。|
| IN|IN运算符用于将值与已指定的文字值列表进行比较。|
| LIKE|LIKE运算符用于使用通配符运算符将值与类似值进行比较。|
| NOT|NOT运算符反转使用它的逻辑运算符的含义。 例如：NOT EXISTS, NOT BETWEEN, NOT IN等等，这是一个否定运算符。 |
| OR|OR运算符用于组合SQL语句的WHERE子句中的多个条件。|
| IS NULL|IS NULL运算符用于将值与NULL值进行比较。|
| UNIQUE|UNIQUE运算符搜索指定表的每一行的唯一性(无重复项)。|

## SQL 选择数据库 USE语句
当SQL Schema中有多个数据库时，在开始操作之前，需要选择一个执行所有操作的数据库。
SQL USE语句用于选择SQL架构中的任何现有数据库。
USE语句的基本语法如下所示 :

```
USE tablename;
```

## SQL LIKE 运算符
在WHERE子句中使用LIKE运算符来搜索列中的指定模式。 
有两个通配符与LIKE运算符一起使用：
％ - 百分号表示零个，一个或多个字符
_ - 下划线表示单个字符

## SQL IN 运算符
IN运算符允许您在WHERE子句中指定多个值。
IN运算符是多个OR条件的简写。

SQL IN 语法
```
SELECT * FROM table WHERE a IN (value1, value2, ...);
SELECT * FROM table WHERE a IN (SELECT STATEMENT);
```

## SQL BETWEEN 运算符
BETWEEN运算符用于选取介于两个值之间的数据范围内的值。
BETWEEN运算符选择给定范围内的值。值可以是数字，文本或日期。
BETWEEN运算符是包含性的：包括开始和结束值，且开始值需小于结束值。 

SQL BETWEEN 语法

```
SELECT * FROM table WHERE a BETWEEN value1 AND value2;
SELECT * FROM table WHERE a NOT BETWEEN value1 AND value2;
```

## SQL INNER JOIN 关键字（内部连接）
内部链接INNER JOIN关键字选择两个表中具有匹配值的记录。
INNER JOIN 与 JOIN 是相同的。
SQL INNER JOIN 语法 (取交集) 

```
SELECT column_name(s)  FROM table1 INNER JOIN table2 ON table1.column_name = table2.column_name;
```

## SQL 左连接 LEFT JOIN 关键字
SQL左链接LEFT JOIN关键字返回左表（表1）中的所有行，即使在右表（表2）中没有匹配。如果在正确的表中没有匹配，结果是NULL。
在一些数据库中，LEFT JOIN称为LEFT OUT ER JOIN。
SQL LEFT JOIN 语法（取左）

```
SELECT column_name(s) 
FROM table1 
LEFT JOIN table2 
ON table1.column_name=table2.column_name;               
```

## SQL右连接 RIGHT JOIN 关键字
SQL右链接 RIGHT JOIN 关键字返回右表（table2）的所有行，即使在左表（table1）上没有匹配。如果左表没有匹配，则结果为NULL。
在一些数据库中，RIGHT JOIN 称为 RIGHT OUTER JOIN。
SQL RIGHT JOIN 语法(取右)

```
SELECT column_name(s)
FROM table1
RIGHT JOIN table2 
ON table1.column_name = table2.column_name;
```
## SQL FULL OUTER JOIN 关键字
当左（表1）或右（表2）表记录匹配时，FULL OUTER JOIN关键字将返回所有记录。 
注意： FULL OUTER JOIN可能会返回非常大的结果集！ 
SQL FULL OUTER JOIN 语法

```
SELECT column_name(s)
FROM table1
FULL OUTER JOIN table2 
ON table1.column_name = table2.column_name;
```
## SQL自连接
自联接是一种常规联接，但表本身是连接的。 
Self JOIN语法

```
SELECT column_name(s)
FROM table1 T1, table1 T2
WHERE condition;
```

**😒😒😒**
**有时间再整。。。。。。。。。。。。**