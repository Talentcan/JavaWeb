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
操作数据库：CRUD  
1.C(Create)：创建  
  - 创建数据库:  
    - create database 数据库名称  
  - 创建数据库，判断是否存在，并指定字符集  
    - create database if not exists 数据库名称 character set 指定的字符集;  
    - create database if not exists db2 character set gbk;  

2.R(Retrieve)：查询  
  - 查询所有数据库的名称  
    - show databases;  
  - 查询某个数据库的字符集：查询某个数据库的创建语句  
    - show create database mysql;  

3.U(Update)：修改  

4.D(Delete)：删除  

5.使用数据库  



