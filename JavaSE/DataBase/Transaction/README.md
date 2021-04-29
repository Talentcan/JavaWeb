# 事务
1.事务的基本介绍  
  * 概念：如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。
  * 操作
    * 1.开启事务：start transaction
    * 2.回滚：rollback
    * 3.提交：commit
    * 4.数据库中事务提交的两种方式
      * 自动提交 
        * 在MySQL数据库中事务默认自动提交
        * 一条DML(增删改)语句会自动提交一次事务，数据会被持久化更新
      * 手动提交
        * Oracle 数据库默认是手动提交事务
        * 需要先开启事务，再提交，如果没有提交，数据不会被持久化更新，在没提交前推出，系统默认回滚，不会保存修改
      * 修改事务的默认提交方式
        * 1.查看事务的默认提交方式：SELECT @@autocommit;  -- 1 代表自动提交，0 代表手动提交
        * 2.修改默认提交方式：SET @@autocommit=0;
```
-- 创建一个新的表
create table account (
  id int primary key auto_increment,
  name varchar(10),
  balance double
);

-- 添加数据
insert into account(name,balance) values ('zhangsan',1000),('lisi',1000);
```
```
事务的案例：张三给李四转账500
分析：
1.判断张三的余额是否大于500
2.如果大于，张三账户-500
3.李四账户+500
事务的概念是其中有一步执行不成功，整个事务就执行失败，不然会造成错误
未开启事务的代码：
-- 张三账户 -500
update account set balance = balance-500 where name = 'zhangsan';
-- 李四账户 +500
-- 若在这一步添加一条错误代码，则上一步执行，下一步未执行，则会出现错误
update account set balance = balance+500 where name = 'lisi';

-- 开启事务
START TRANSACTION;
-- 张三账户 -500
update account set balance = balance-500 where name = 'zhangsan';
-- chucuola.... 
-- 李四账户 +500
update account set balance = balance+500 where name = 'lisi';
-- 发现出错要进行回滚，回滚到这个事务开始所在的位置
ROLLBACK;
-- 执行结束，没有异常，则提交事务
COMMIT;

```
2.事物的四大特征  
  * 原子性：事务是不可分割的最小操作单位，要么同时成功，要么同时失败
  * 持久性：如果事务一旦提交或者回滚后，数据库会持久化的保存数据
  * 隔离性：多个事务之间相互独立，不产生相互影响
  * 一致性：事务操作前后，数据总量不变

3.事物的隔离级别  
  * 概念：多个事务之间隔离，相互独立，但是如果多个事务操作同一批数据，则会引发一些问题，设置不同的隔离级别就可以解决这些问题
  * 存在问题
    * 1.脏读：一个事务读取到另一个事务中没有提交的数据，这相当危险，可能导致所有的操作都被回滚
    * 2.不可重复读：在同一个事务中，两次读取到的数据不同
      * 幻读：事务在操作过程中进行两次查询，第二次查询的结果包含了第一次查询中未出现的数据或者缺少了第一次查询中出现的数据（这里并不要求两次查询的SQL语句相同）。这是因为两次查询过程中有一个事务插入数据造成的
      * 虚读：事务T1读取某一数据后，事务T2对其做了修改，当事务T1再次读取该数据时得到了与前一次不同的结果
    * 3.更新丢失：两个事务同时更新一行数据，一个事务对数据的更新把另一个事务对数据的更新覆盖了。这是由于系统没有执行任何的锁操作，因此并发事务没有被隔离开来
  * 隔离级别
    * 1.






