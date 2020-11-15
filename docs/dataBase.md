# 数据库

## MySQL

### 索引

#### 索引底层实现

#### 索引存储方式

- 聚簇索引与非聚簇索引
  - 聚簇索引的叶子节点中，包含了一个完整的记录行。
  - 非聚簇索引中因为不含有完整的数据信息，查找完整的数据记录需要回表，所以一次查询操作实际上要做两次索引查询。

参考：https://www.dyxmq.cn/databases/mysql/clustered-nonclustered-union-and-unique-indexes-in-mysql.html