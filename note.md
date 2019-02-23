1. sql客户端开启事务如下：
```sql
    start transaction;
    INSERT INTO t_user(name, sex, age) VALUES('Mary', '女', 20);
    INSERT INTO t_user VALUES(null, 'Tom', '男', 22);
    COMMIT;
```
2. truncate table xx删除表的所有数据，会将AUTO_INCREMENT设置为1，不删除表结构；  
drop table会删除表结构和数据；    
delete不加where语句也删除所有数据，不会设置AUTO_INCREMENT。  
但truncate、drop是DDL语句，ddl语句即时生效，不受事务影响；  delete是DML语句，受事务影响，如果有事务需要事务提交才生效。