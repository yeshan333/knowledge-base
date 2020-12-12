# 数据库

## MySQL

### 常用指令

- `desc table_name`：查看表结构
- `explain sql_statement`：查看 sql 语句是如何执行的
- `show processlist`：查看数据库连接状况
- `select @@datadir`：查看数据文件存储位置

>- 详解 explain：https://mp.weixin.qq.com/s/izryJDfT5pR0_ljO-l_fyw

### 日志系统

#### 引擎层的 redo log 与 Server 层的 bin log

> WAL 技术：Write-Ahead Logging 先写日志。「先写日志，再写磁盘，日志也是写到磁盘的，不过是以顺序的方式（顺序写入）」

当有一条记录需要更新的时候，InnoDB 引擎就会先把记录写到 redo log 里面，并更新内存，这个时候更新就算完成了。同时，InnoDB 引擎会在适当的时候，将这个操作记录更新到磁盘里面，而这个更新往往是在系统比较空闲的时候做。

#### redo log 与 bin log 的区别

关注点：记录更新时刻

- 1、redo log 是 InnoDB 引擎特有的；binlog 是 MySQL 的 Server 层实现的，所有引擎都可以使用。
- 2、redo log 是物理日志，记录的是“在某个数据页上做了什么修改”；binlog 是逻辑日志，记录的是这个语句的原始逻辑，比如“给 ID=2 这一行的 c 字段加 1 ”。
- 3、redo log 是循环写的，空间固定会用完；binlog 是可以追加写入的。“追加写”是指 binlog 文件写到一定大小后会切换到下一个，并不会覆盖以前的日志。

#### redo log 的两阶段提交

### 数据库事务

>数据库事务( transaction)是访问并可能操作各种数据项的一个数据库操作序列，这些操作要么全部执行,要么全部不执行，是一个不可分割的工作单位。 事务由事务开始与事务结束之间执行的全部数据库操作组成。

#### 事务特性ACID

- 原子性（Atomicity）
- 一致性（Consistency）
- 隔离性（Isolation）
- 持久性（Durability）

#### 事务隔离级别与 MVCC

>MVCC：多版本并发控制（MVCC），同一条记录在系统中可以存在多个版本。

查看当前数据库设置的事务隔离级别：

```mysql
show variables like 'transaction_isolation';
```

- 读未提交：一个事务还未提交，它所做的变更就可以被别的事务看到；
- 读提交：一个事务提交之后，它所做的变更才可以被别的事务看到；
- 可重复读：一个事务执行过程中看到的数据是一致的。未提交的更改对其他事务是不可见的；
- 串行化：对应一个记录（record row）会加读写锁，出现冲突的时候，后访问的事务必须等待前一个事务执行完成才能继续执行。

从上到下并行性能依次降低，安全性依次提高。

> 参考：[极客实践MySQL实战-事务隔离：为什么你改了我还看不见？](https://time.geekbang.org/column/article/68963)

### 主键与索引

- 主键可以由多个字段组成，组成复合主键，同时主键肯定也是唯一索引。
- 数据表中只允许有一个主键，但是可以有多个索引。
- 唯一索引表示该索引值唯一，可以由一个或几个字段组成，一个表可以有多个唯一索引。

### 索引

#### 索引底层实现（索引模型）

- 有序数组索引：只适用于静态存储引擎
- 哈希表索引：适用于等值查询场景
- B 树索引：支持范围查询。B 树索引的节点会存储记录。
- InnoDB B+ 树索引：支持范围查询，但相比于 B 树，B+ 树内节点不存储数据，减少磁盘 I/O（降低局部性原理的影响）。主键索引（即聚簇索引）叶子节点存储整行数据。非主键索引的叶子节点存储的是主键值，非主键索引也称为二级索引。

#### 索引存储方式

- 聚簇索引与非聚簇索引
  - 聚簇索引的叶子节点中，包含了一个完整的记录行。
  - 非聚簇索引中因为不含有完整的数据信息，查找完整的数据记录需要回表，所以一次查询操作实际上要做两次索引查询。

参考：https://www.dyxmq.cn/databases/mysql/clustered-nonclustered-union-and-unique-indexes-in-mysql.html

#### 联合索引与最左前缀原则

#### 索引创建规则

1、表的主键、外键必须有索引；
2、数据量超过300的表应该有索引；
3、经常与其他表进行连接的表，在连接字段上应该建立索引；
4、经常出现在Where子句中的字段，特别是大表的字段，应该建立索引；
5、索引应该建在选择性高的字段上；
6、索引应该建在小字段上，对于大的文本字段甚至超长字段，不要建索引；
7、复合索引的建立需要进行仔细分析；尽量考虑用单字段索引代替
8、频繁进行数据操作的表，不要建立太多的索引；
9、删除无用的索引，避免对执行计划造成负面影响；

注意点：

1. 限制表上的索引数目。对一个存在大量更新操作的表，所建索引的数目一般不要超过3个，最多不要超过5个。索引虽说提高了访问速度，但太多索引会影响数据的更新操作。
2. 避免在取值朝一个方向增长的字段（例如：日期类型的字段）上，建立索引；对复合索引，避免将这种类型的字段放置在最前面
3. 对复合索引，按照字段在查询条件中出现的频度建立索引
4. 删除不再使用，或者很少被使用的索引。

#### 索引失效情形

1.有or必全有索引;
2.复合索引未用左列字段;
3.like以%开头;
4.需要类型转换;
5.where中索引列有运算;
6.where中索引列使用了函数;
7.如果mysql觉得全表扫描更快时（数据少）;

### MySQL 中的那些锁

- 全局锁：整个数据库加锁，使用`Flush tables with read lock (FTWRL)`让数据库只读，适用于全库备份场景；
- 表级锁
  - 表锁：
  - 元数据锁：访问表的时候会自动加上，写锁互斥
- 行锁，行锁是在引擎层由各个引擎自己实现。

#### 乐观锁与悲观锁

悲观锁：假定会发生并发冲突，屏蔽一切可能违反数据完整性的操作。
乐观锁：假设不会发生并发冲突，只在提交操作时检查是否违反数据完整性。