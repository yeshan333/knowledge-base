# 不止于后端

## SSO 单点登录系统的实现

- https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/authority-certification/sso.md
- [系统的讲解 - SSO单点登录](https://www.imooc.com/article/286710)

## 消息队列


## 分布式缓存

> refs: 《300分钟吃透分布式缓存-陈波》

**缓存知识点全景图**

![缓存知识点全景图](https://cdn.jsdelivr.net/gh/ssmath/mypic/img20200716171358.png)

**与 CPU 缓存相似的架构**

![缓存架构](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200716174555.png)

### 缓存原理

- 基本思想
  - 时间局限性原理：被获取过一次的数据在未来（短时间内）会被多次引用
  - 空间局部性原理：被访问过的一个数据，它相邻的数据也很快会被访问。即最近访问过数据附近的数据很快会被访问到
  - 以空间换时间：开辟一块高速独立空间，提供高效访问
  - 性能成本 Tradeoff(权衡)：维持相同数据规模的存储以及访问，性能越高延迟越小，成本越高。系统架构设计时需要权衡系统性能和开发运行成本

![等成本比对](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200716173458.png)

#### 缓存读写模式

- Cache Aside（旁路缓存）

![Cache Aside模式](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200716195047.png)

Cache Aside 模式写操作时是直接删除 Cache 的，靠 DB 更新 Cache。读操作时，如果 Cache 不存在，则读 DB，靠 DB 更新 Cache。

- Read/Write Through（读写穿透）

![Read/Write Through](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200716195158.png)

写操作时，Cache 中没有数据则不更新；读操作时命中数据直接返回，否则先从 DB 加载数据到 Cache 后再响应。此模式下，可将**业务逻辑与存储服务分离**。

- Write Behind Caching（异步缓存写入）

![Write Behind Caching](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200716202034.png)

数据更新时，Read/write Through 是同步更新 Cache 和 DB，而 Write Behind Caching 则是只更新缓存，不直接更新 DB，而是改为**异步批量的方式来更新 DB**。

一般用于合并写请求的业务，比如对一些计数业务，一条 Feed 被点赞 1万 次，如果更新 1万 次 DB 代价很大，而合并成一次请求直接加 1万，则是一个非常轻量的操作。

### 缓存设计中的七大经典问题及解决方案

### 缓存失效、穿透、雪崩

- 缓存失效
  - 原因：同一批数据（机票等）预设值缓存过期时间相同
  - 解决方案：设置同批数据，过期时间=base时间+随机时间
- 缓存穿透
  - 原因：系统设计时对特殊访问，异常访问路径考虑相对欠缺（例如大量特殊访问不存在的 key）。
  - 解决方案
    - 1、：虽然 key 不存在，但记录 key 到 Cache，但是 key 对应的 value 是一个特殊值。（需要注意让这些 key 的存活时间尽可能短）
    - 2、：使用布隆过滤器判断 key（10亿左右，1.2G内存暂用） 是否存在
- 缓存雪崩：部分缓存节点不可用，导致导致整体缓存体系甚至服务系统不可用
  - 原因
    - 1、：缓存不支持 rehash ，由于较多缓存节点不可用，请求穿透至 DB，使 DB 过载不可用，最终导致整体不可用
    - 2、：缓存支持 rehash，流量洪峰来临，引发部分缓存节点 Crash（崩溃），因 rehash 扩散到其他节点，导致整体不可用
  - 解决方案
    - 1、：缓存副本
    - 2、：监控 DB 请求，响应变慢关闭读开关，等待回复再打开
    - 3、：缓存实时监控，阈值报警

> 布隆过滤器：https://zhuanlan.zhihu.com/p/95275499，https://zhuanlan.zhihu.com/p/31498003

### 缓存数据不一致和并发竞争

- 缓存数据不一致问题
  - 原因
    - 1、：DB 更新后，写缓存失败，导致缓存中存在的是老数据
    - 2、：系统采用一致性 Hash 分布，同时采用 rehash 自动飘移策略，节点多次上线产生脏数据
    - 3、：缓存有多个副本，某个副本更新失败
  - 解决方案
    - 1、：Cache 更新失败，进行重试，重试仍失败将失败 key 写入队列机服务，待缓存访问恢复后，将 key 从缓存删除。key 再次被查询时，再从 DB 加载
    - 2、：让缓存数据及早过期
    - 3、：不采用 rehash 漂移策略，采用缓存分层策略

- 数据并发竞争：高并发访问场景，一旦缓存访问没有找到数据，大量请求就会并发查询 DB，导致 DB 压力增大的现象
  - 原因：多线程/进程并发请求相同 key，但是 key miss，直怼 DB
  - 解决方案
    - 1、：引入全局锁，对 miss 的 key 加锁，直 DB 回种缓存
    - 2、：缓存备份

### Hot Key && Big Key

- Hot Key
  - 问题：突发热点事件，访问 Hot Key，导致流量全打在同一缓存节点，导致缓存访问变慢甚至 Crash
  - 解决方案
    - 1、：对于突发事件，使用 Spark 对流任务进行实时分析，及时发现 Hot Key。对于已发生事件逐步演进为热门事件的，使用 Hadoop 对批处理任务离线计算，找出历史数据种的高频 Hot Key。找到 Hot Key 后进行分散处理，如（key、key#1、key#2...），随机访问这些 keys
    -2、：多副本 + 多级结合

- Big Key：即 Key 对应的 Value 过大，读写加载容易超时
  - 原因：

## RESTful APIs

RESTful APIs典型场景

![RESTful APIs典型场景](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200210193225.png)

[细说API – 重新认识RESTful](https://insights.thoughtworks.cn/api-restful/)

[细说API – 文档和前后端协作](https://insights.thoughtworks.cn/api-document-front-back-end-collaboration/)

## 认证、授权和凭证

!> 认证(authentication)、授权(authorization)和凭证(credentials)

[细说API – 认证、授权和凭证](https://insights.thoughtworks.cn/api-2/)

## IaaS、PaaS、SaaS

![IaaS、PaaS、SaaS](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200210192223.png)

参考：[DevOps 实战：Jenkins Docker](https://cloud.tencent.com/developer/article/1575521)

PS：感觉这篇文章也可以叫从 Docker 看云计算的演进

## Python

### shallow copy&deep copy