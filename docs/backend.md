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

### 缓存数据不一致和并发竞争

### Hot Key && Big Key

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