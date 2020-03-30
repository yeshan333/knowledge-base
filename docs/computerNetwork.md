# 计算机网络基础

## OSI七层模型、TCP/IP四层模型

![OSI七层模型](https://i.loli.net/2020/03/22/RSLPkrfd3AsmcyC.jpg)

![OSI七层模型、TCP/IP四层模型](https://i.loli.net/2020/03/22/qthHTNlXyOvEfm3.png)

## HTTP

- **HTTP 1.0**：一个 TCP 连接只可以发送一个 HTTP 请求，每次请求都需要重新建立和断开 TCP 连接
- **HTTP 1.1**：引入持久连接，使用 Header 头 `Connection: keep-alive`维持持久连接，一个连接可发送多个 HTTP 请求（但一个时刻只能发送一个），response 使用  `Connection: close` Header 断开连接
- **HTTP 2.0**：多路复用，一个 TCP 连接中可同时完成多个 HTTP 请求

>参考：
>[HTTP/1.x 的连接管理](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Connection_management_in_HTTP_1.x#HTTP_%E6%B5%81%E6%B0%B4%E7%BA%BF)
>[你猜一个 TCP 连接上面能发多少个 HTTP 请求](https://zhuanlan.zhihu.com/p/61423830)

### Session与Cookie

- Session 是在服务端保存的一个数据结构，用来跟踪用户的状态，这个数据可以保存在集群、数据库、文件中；
- Cookie 是客户端保存用户信息的一种机制，用来记录用户的一些信息，也是实现 Session 的一种方式。

## TCP三次握手建立TCP连接

![TCP三次握手](https://i.loli.net/2020/03/22/vRaQ5k26BiFbZqg.png)

- **序列号 seq**：所发送字节流的第一个字节的编号
- **确认号 ack**：期望收到的下一个报文段的序号。
- **ACK**：控制位 ACK=1 表示数据已收到，TCP 规定，在连接建立后所有传送的报文段都必须把 ACK 置 1
- **同步 SYN**：控制位，在连接建立时用来同步序号。当 SYN=1，ACK=0 时表示这是一个连接请求报文段。若对方同意建立连接，则响应报文中 SYN=1，ACK=1。


?> **为什么需要三次握手**：为了防止已失效的连接请求报文段突然又传送到了服务端，占用服务器资源。

## TCP四次挥手结束TCP连接

![TCP四次挥手](https://i.loli.net/2020/03/23/RFQ5LSwc8EmJBeo.png)

- **终止 FIN**：控制位，用来释放一个连接，当 FIN=1 时，表示此报文段的发送方的数据已发送完毕，并要求释放连接。