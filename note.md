1. sql客户端开启事务如下：
```sql
    start transaction;
    INSERT INTO t_user(name, sex, age) VALUES('Mary', '女', 20);
    INSERT INTO t_user VALUES(null, 'Tom', '男', 22);
    COMMIT;
```
> START TRANSACTION或BEGIN都是显式地开启一个事务；
2. `truncate table xx`删除表的所有数据，会将AUTO_INCREMENT设置为1，不删除表结构；  
drop table会删除表结构和数据；    
delete不加where语句也删除所有数据，不会设置AUTO_INCREMENT。  
但truncate、drop是DDL语句，ddl语句即时生效，不受事务影响；  delete是DML语句，受事务影响，如果有事务需要事务提交才生效。
3. savepoint
- SAVEPOINT savepoint_name 在当前事务中定义一个新的保存点
- ROLLBACK TO SAVEPOINT savepoint_name 在commit之前回滚到一个保存点
```sql
BEGIN;
INSERT INTO t_user(name, sex, age) VALUES('111', '女', 20);
SAVEPOINT my_savepoint;
INSERT INTO t_user(name, sex, age) VALUES('222', '女', 20);
ROLLBACK TO SAVEPOINT my_savepoint;
INSERT INTO t_user(name, sex, age) VALUES('333', '女', 20);
COMMIT;
```
> 以上sql会插入name为111和333的两条记录，不会插入222.


999. [jdbc事务、保存点实践源码](/Java-deep-study/code/jdbc-batch-operate)
