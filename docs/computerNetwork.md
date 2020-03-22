# 计算机网络基础

## OSI七层模型、TCP/IP四层模型

![OSI七层模型](https://i.loli.net/2020/03/22/RSLPkrfd3AsmcyC.jpg)

![OSI七层模型、TCP/IP四层模型](https://i.loli.net/2020/03/22/qthHTNlXyOvEfm3.png)

## HTTP1.0与HTTP1.1


## TCP三次握手建立TCP连接

![TCP三次握手](https://i.loli.net/2020/03/22/vRaQ5k26BiFbZqg.png)

- **序列号 seq**：所发送字节流的第一个字节的编号
- **确认号 ack**：期望收到的下一个报文段的序号。
- **ACK**：控制位 ACK=1 表示数据已收到，TCP 规定，在连接建立后所有传送的报文段都必须把 ACK 置 1


?> **为什么需要三次握手**：为了防止已失效的连接请求报文段突然又传送到了服务端，占用服务器资源。

## TCP四次挥手结束TCP连接