# 计算机网络基础

## OSI七层模型、TCP/IP四层模型

![OSI七层模型](https://i.loli.net/2020/03/22/RSLPkrfd3AsmcyC.jpg)

![OSI七层模型、TCP/IP四层模型](https://i.loli.net/2020/03/22/qthHTNlXyOvEfm3.png)

## HTTPS

![HTTPS 原理](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20210314232935.png)

- 参考：
  - https://cattail.me/tech/2015/11/30/how-https-works.html
  - [可怕，原来 HTTPS 也没用](https://mp.weixin.qq.com/s?__biz=MzU1NjgwNTExNQ==&mid=2247489276&idx=1&sn=5aad30af3131a31d6340d5e5bf85900f&chksm=fc3e2868cb49a17ec91834b86be3068f11d6cfe612a5a7d83a2a880c03b9ea9b4d8028a79a21&mpshare=1&scene=23&srcid=0314VCiQsRHCVW2zqpvJGiVo&sharer_sharetime=1615707706221&sharer_shareid=4d09c35f897e38c8ae8043ee7861db58#rd)

## HTTP

- **HTTP 1.0**：一个 TCP 连接只可以发送一个 HTTP 请求，每次请求都需要重新建立和断开 TCP 连接
- **HTTP 1.1**：引入持久连接，使用 Header 头 `Connection: keep-alive`维持持久连接，一个连接可发送多个 HTTP 请求（但一个时刻只能发送一个），response 使用  `Connection: close` Header 断开连接
- **HTTP 2.0**：
  - 相对于之前头部信息使用文本传输，HTTP2将所传送信息分为更小的二进制帧，头部信息被封装到Header Frame，body 被封装到 Data Frame。
  - 多路复用（http请求量大的场景下才明显），在一个 TCP 连接中可以存在多条流，一条 stream对应一个 request。stream 由 frame 组成，frame 会有标识说明它属于哪个 stream。
  - 解决队头阻塞：浏览器限制了同一个域名下的请求数量，当页面中需要请求很多资源的时候，队头阻塞（Head of line blocking）会导致在达到最大请求数量时，剩余的资源需要等待其他资源请求完成后才能发起请求。

>参考：
>[HTTP/1.x 的连接管理](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Connection_management_in_HTTP_1.x#HTTP_%E6%B5%81%E6%B0%B4%E7%BA%BF)
>[你猜一个 TCP 连接上面能发多少个 HTTP 请求](https://zhuanlan.zhihu.com/p/61423830)
>[HTTP2 讨论](https://www.zhihu.com/question/34074946)
>[了解HTTP演进](https://mp.weixin.qq.com/s?__biz=MzAwMjg1NjY3Nw==&mid=2247496973&idx=1&sn=78e6d173e44a2efeabceddbcca38b5d8&chksm=9ac6b687adb13f91cb1ae2508bae118c2fa6ab0134dc5c51ced6cba4a092e325c8848571655c&mpshare=1&scene=23&srcid=0906aP8DTMmYPQaFV63Ku1oH&sharer_sharetime=1599442256662&sharer_shareid=4d09c35f897e38c8ae8043ee7861db58#rd)

### 长短连接

- [gRPC 长连接在微服务业务系统中的实践](https://mp.weixin.qq.com/s/LKGzc6XBAWYdskVQQJFLHw)

### Session与Cookie

- Session 是在服务端保存的一个数据结构，用来跟踪用户的状态，这个数据可以保存在集群、数据库、文件中；
- Cookie 是客户端保存用户信息的一种机制，用来记录用户的一些信息，也是实现 Session 的一种方式。

## IP

- IP 私有网段，有A,B,C三个地址段：
  - 10.0.0.0/8:10.0.0.0-10.255.255.255
  - 172.16.0.0/12:172.16.0.0-172.31.255.255
  - 192.168.0.0/16:192.168.0.0-192.168.255.255

## TCP三次握手建立TCP连接

![TCP三次握手](https://i.loli.net/2020/03/22/vRaQ5k26BiFbZqg.png)

- **序列号 seq**：所发送字节流的第一个字节的编号
- **确认号 ack**：期望收到的下一个报文段的序号。
- **ACK**：控制位 ACK=1 表示数据已收到，TCP 规定，在连接建立后所有传送的报文段都必须把 ACK 置 1
- **同步 SYN**：控制位，在连接建立时用来同步序号。当 SYN=1，ACK=0 时表示这是一个连接请求报文段。若对方同意建立连接，则响应报文中 SYN=1，ACK=1。


?> **为什么需要三次握手**：为了防止已失效的**连接请求报文段**突然又传送到了服务端，占用服务器资源。（如果是两次握手，服务端接收到的可能是已经超时才传到连接请求报文，客户端已经不承认了）。

### 三次握手流程简述

- 第一次握手：server 端处于 LISTEN 状态，client 端向 server 端发送 SYN 包后进入 SYN_SEND 状态；

- 第二次握手：server 端收到 client 端的 SYN 包后，ACK client 端的 SYN 包并且自己也发送个 SYN 包，server 端进入 SYN-RECV 状态；

- 第三次握手：client端 收到 server 端的 ACK + SYN 包后，向服务端发送 ACK 包，发送完毕后，server 端和 client 进入 ESTABLISHED 状态。

> 参考：https://www.nowcoder.com/tutorial/94/a6035e5453f946aba0615705f94ca1e2w'coa'owcoao

## TCP四次挥手结束TCP连接

![TCP四次挥手](https://i.loli.net/2020/03/22/ApsXC7E1Mwzdqae.png)

一二次握手（客户端测连接关闭），三四次握手（服务端一侧连接关闭）。

- **终止 FIN**：控制位，用来释放一个连接，当 FIN=1 时，表示此报文段的发送方的数据已发送完毕，并要求释放连接。

!> 服务端的 CLOSE-WAIT 状态：为了让服务器端发送还未传送完毕的数据，传送完毕之后，服务器会发送 FIN 连接释放报文。

!> 客户端的 TIME—WAIT 状态：等待一个时间计时器设置的时间 2MSL(maximium segment lifetime，最长报文寿命)。确保最后一个确认报文段能够到达，同时让本连接持续时间内所产生的所有报文段都从网络中消失，使得下一个新的连接不会出现旧的连接请求报文段。

参考：[跟着动画来学 TCP 三次握手和四次挥手](https://juejin.im/post/5b29d2c4e51d4558b80b1d8c)

# 面试题

参考：https://www.bilibili.com/video/BV1gk4y1o7pX

## 1、请详细介绍下 TCP 的三次握手机制，为什么需要三次握手？

- 为什么需要握手，为什么是三次握手？

因为 TCP 有个重要的特性即为**可靠性**，发送方发了消息，接受方需回应收到了，不然就重发。通过对消息进行编号（序列号sequence，不能从 0 开始）证明消息发过去了。握手的一个重要作用就是同步序列号，还可以同步滑动窗口和MSL等。

为什么是三次握手？以稳定性为着眼点，我们会认为是 4 次握手（关连接的时候就是 4 次），关连接的时候连接可以处于半打开状态继续传输消息（server 关连接了，但是 client 没有关连接，client 仍然可以长时间的去发送消息「只要server没有强制关闭连接」），但是建立连接的时候不能是半打开状态。如果是两次呢？如果是两次握手，服务端接收到的可能是已经超时才传到连接请求报文，客户端已经不承认了，此时服务端的资源会被占用。

## 2、在地址栏输入URL后，网络世界发生了什么？

看点：

- DNS查询、缓存、代理
- HTTP 请求编码，地址输入后，HTTP 请求的格式是怎么样的
- 报文消息如何传输到服务器（网络分层，各层解决了什么）
- 等等

## 3、TCP 和 UDP 的区别

- TCP
  - 传递任意长度消息，面向字节流的协议（字节流，就是发的是一个流，没头没尾。TCP 自己维护流状态）
  - 可靠
  - 流量控制
  - 拥塞控制
  - TCP 是一个有状态的服务，有状态可以理解为：我记录了哪些发送了，哪些没有发送，哪些接收到了，哪些没接收到，应该接收哪个了，

- UDP
  - 一对多
  - 效率高，header短，有效信息占比高
  - 简单
  - 实时性好
    - 无队头阻塞

!> HTTP1.1 队头阻塞：一个 TCP 连接同时传输10个请求时，当某一个请求丢失，TCP协议会阻塞后面几个请求，然后进行数据重传。虽然TCP有快速重传等机制来缓解这个问题，但是只能是缓解。

- [怎么用 UDP 实现 TCP？](https://mp.weixin.qq.com/s/P01PBMQ_3bmOpW4eT2pqdA)

### TCP 拥塞控制核心算法

- 慢启动：发送方向接收方发送数据一般是指数级增长的（1个单位数据 -> 2个单位数据 —> 4个...），通过这个过程不断尝试网络的拥塞程度，超出阈值会导致网阔拥塞；
- 拥塞避免：指数级增长不是无限的，到达某个限制（阈值）之后，指数级增长变为线性增长；
- 快速重传：发送方每一次发送时都会设置一个超时计时器，超时后即认为数据丢失，需要重发；
- 快速恢复：在快重传的基础上，发送方重新发送数据时，也会启动一个定时计时器，如果收到确认消息则进入拥塞避免阶段，如果仍然超时，则回到慢启动阶段。

## 4、使用 HTTP 长连接有何有优点

- 减少握手次数，每次连接建立与断开共七次握手，4 个请求就有 28 次握手，长连接只有 7 次
- 减少慢启动影响：虽然 TCP 可以传递任意长度的消息，因为网络带宽有限，所需发送时的速率会从低转高。
- 缺点：可能会遭遇队头阻塞

> 短连接，HTTP header 的 conection为 close。

## 5、服务器的最大并发连接数是多少

端口号并不能限制并发连接数，端口号的作用是在网络连接中标识应用层的进程，一个服务端进程可服务于 n 个客户远程进程。

!> 并发连接数由 TCP 四元组决定。

TCP 四元组：IP 报头（源 IP 和 目标 IP），TCP 报头（源端口和目的端口）「端口与进程关联」。服务端的 IP 和端口一般不可变，所以连接数收客户端 IP 和端口限制。

$$ TCP 最大连接数 = 客户端 IP 数 \times 客户端端口数 $$

对于 IPv4，即为 $ 2^{32+16} $（16 bits 存储端口号，32 bits存储 IP 地址）。Linux 系统端口开放受限制，可能需要手动打开。

## 6、TLS/SSL 协议是怎样保障信息安全的

- PKI 证书体系
- 密钥交换协议（握手谈好使用的协议）
- 对称加密算法交换密钥

## 网络安全

### XSS

> 参考：[美团技术团队-前端安全系列（一）：如何防止XSS攻击？](https://tech.meituan.com/2018/09/27/fe-security.html)

Cross-Site Scripting（跨站脚本攻击）简称 XSS，是一种代码注入攻击。攻击者通过在目标网站上注入恶意脚本，使之在用户的浏览器上运行。利用这些恶意脚本，攻击者可获取用户的敏感信息如 Cookie、SessionID 等，进而危害数据安全。

#### 攻击特点

- 后端 RD 视角
  - 存储型 XSS：常见于带有用户保存数据的网站功能，如论坛发帖、商品评论、用户私信等。
  - 反射型 XSS：反射型 XSS 漏洞常见于通过 URL 传递参数的功能，如网站搜索、跳转等。
  - 存储型 XSS 的恶意代码存在数据库里，反射型 XSS 的恶意代码存在 URL 里。
- 前端 RD
  - DOM 型 XSS：DOM 型 XSS 攻击中，取出和执行恶意代码由浏览器端完成，属于前端 JavaScript 自身的安全漏洞，而其他两种 XSS 都属于服务端的安全漏洞。

#### 防护策略

- 存储与反射型
  - 纯前端渲染
  - HTML 转义
- DOM 型
  - 不要把不可信的数据作为 HTML 插到页面上

### CSRF 攻击与防护

> 参考：[美团技术团队-前端安全系列（二）：如何防止CSRF攻击？]()

CSRF（Cross-site request forgery）跨站请求伪造：攻击者诱导受害者进入第三方网站，在第三方网站中，向被攻击网站发送跨站请求。利用受害者在被攻击网站已经获取的注册凭证，绕过后台的用户验证，达到冒充用户对被攻击的网站执行某项操作的目的。

#### 攻击特点

- 攻击一般发起在第三方网站，而不是被攻击的网站。被攻击的网站无法防止攻击发生。
- 攻击利用受害者在被攻击网站的登录凭证，冒充受害者提交操作；而不是直接窃取数据。
- 整个过程攻击者并不能获取到受害者的登录凭证，仅仅是“冒用”。
- 跨站请求可以用各种方式：图片URL、超链接、CORS、Form提交等等。部分请求方式可以直接嵌入在第三方论坛、文章中，难以进行追踪。

#### 防护策略

- 阻止不明外域的访问
  - 同源检测
  - Samesite Cookie
- 提交时要求附加本域才能获取的信息
  - CSRF Token
  - 双重Cookie验证

### Cookies 保护

- SamSite Cookies：https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Set-Cookie/SameSite

