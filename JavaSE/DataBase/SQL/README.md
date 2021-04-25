# SQL
## 什么是SQL
结构化查询语言(Structured Query Language)简称SQL。是一种特殊目的的编程语言，是一种数据库查询和程序设计语言，用于存取数据以及查询、更新和管理关系数据库系统；同时也是数据库脚本文件的扩展名。其实就是定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方。

## SQL通用语法
1.SQL语句可以单行或多行书写，以分号结尾

2.MySQL数据库不区分大小写，但是建议关键字使用大写

3.三种注释
```
单行注释：-- 注释内容（--后需要加一个空格） 或 #注释内容（MySQL特有）
多行注释：/* 注释内容 */ 
```

## SQL分类
1.DDL：数据定义语言，用来定义数据库对象（数据库，表，列等），关键字：create，drop，alter等

2.DML：数据操作语言，用来对数据库中表的数据进行增删改，关键字：insert，delete，update等

3.DQL：数据查询语言，用来查询数据库中表的记录（数据），关键字：select，where等

4.DCL：数据控制语言，用来定义数据库的访问权限和安全级别，及创建用户，关键字：GRANT,REVOKE等

## DDL：操作数据库，表
### 操作数据库：CRUD  
1.C(Create)：创建
  - 创建数据库:  
    - create database 数据库名称;  
  - 创建数据库，判断是否存在，并指定字符集  
    - create database if not exists 数据库名称 character set 指定的字符集;  
    - 如：create database if not exists db2 character set gbk;  

2.R(Retrieve)：查询  
  - 查询所有数据库的名称  
    - show databases;  
  - 查询某个数据库的字符集：查询某个数据库的创建语句  
    - show create database mysql;  

3.U(Update)：修改  
  - 修改数据库的字符集  
    - alter database 数据库名称 character set 字符集名称;  
    - 如：alter database db2 character set utf8;  

4.D(Delete)：删除   
  - 删除数据库  
    - drop database if exists 数据库名称;  

5.使用数据库  
  - 查询当前正在使用的数据库名称  
    - select database();  
  - 使用数据库  
    - use 数据库名称;  


### 操作表
1.C(Create)：创建  
  - 语法：create table 表名(列名1 数据类型,列名2 数据类型,列名3 数据类型),  最后一行的列不用加逗号  
  - 数据类型
    - int 整数类型 age int
    - double 小数类型 score double(5,2) 表示总的有5位，小数有两位，如999.99
    - date 日期类型 只包含年月日 yyyy-MM-dd
    - datetime 日期类型 包含年月日时分秒 yyyy-MM-dd HH:mm:ss
    - timestamp 时间戳类型 包含年月日时分秒 yyyy-MM-dd HH:mm:ss，如果将来不给这个字段赋值或赋值为null，则默认使用当前的系统时间来自动赋值
    - varchar 字符串类型 name varchar（20）表示最大20个字符
```ruby
-- 创建一张学生表
create table student(
  id int,
  name varchar(32),
  age int,
  score double(4,1),
  birthday date,
  insert_time timestamp
  );
```
  - 复制一张表：create table 新表名 like 想要复制的表;
    - 如：create table stu like student;

2.R(Retrieve)：查询  
  - 查询某个数据库中所有的名称
    - show tables;
  - 查询表结构
    - desc 表名;
  - 查询表的字符集
    - show create table 表名;

3.U(Update)：修改  
  - 修改表名
    - alter table 表名 rename to 新的表名;
  - 修改表的字符集
    - alter table 表名 character set 字符集名称;
  - 添加一列
    - alter table 表名 add 列名 数据类型;
  - 修改列的名称和类型
    - alter table 表名 change 列名 新列名 新数据类型; --可以修改列的名称和类型
    - alter table 表名 modify 列名 新数据类型; --只能修改类的数据类型
  - 删除列
    - alter table 表名 drop 列名; 

4.D(Delete)：删除   
  - drop table 表名;
  - drop table if exists 表名;















