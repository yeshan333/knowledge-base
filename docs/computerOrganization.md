# 计算机组成原理基础

![计算机](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200216204537.png)

## 计算机硬件基础架构

### 冯·诺伊曼体系结构

>wiki：[https://zh.wikipedia.org/wiki/冯·诺伊曼结构](https://zh.wikipedia.org/wiki/%E5%86%AF%C2%B7%E8%AF%BA%E4%BC%8A%E6%9B%BC%E7%BB%93%E6%9E%84)

五大基本组件：运算器、控制器、存储器、输入设备和输出设备。

五大组件的应用与设计：**性能**和**功耗**

![冯诺伊曼体系结构](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200216213049.png)

## 计算机系统的性能指标

[基本字长](https://zh.wikipedia.org/zh-hans/%E5%AD%97_(%E8%AE%A1%E7%AE%97%E6%9C%BA))：一次数据操作得基本位数，影响计算得精度、指令的功能

运算速度：
  - 系统[时钟频率](https://zh.wikipedia.org/zh-hans/%E6%97%B6%E9%92%9F%E9%A2%91%E7%8E%87)（CPU外频/基频）：CPU 与外部组件进行数据传输的速度
  - CPU 倍频：CPU内部用来加速工作效能的一个倍数，CPU 与系统总线相差的倍数，$ CPU 主屏 = CPU 外频 \times CPU 倍频 $
  - IPS(Instruction Per Second)：每秒执行指令数
  - CPI(Clock-cycle Per Instruction)：指令平均周期，执行一条指令所需要的时钟周期
  - [FLOPS](https://zh.wikipedia.org/zh-cn/%E6%AF%8F%E7%A7%92%E6%B5%AE%E9%BB%9E%E9%81%8B%E7%AE%97%E6%AC%A1%E6%95%B8)(floating-point operations per second)：每秒浮点运算速度

数据传输率：
  - [带宽](https://zh.wikipedia.org/wiki/%E5%B8%A6%E5%AE%BD)(Bandwidth)，单位时间数据的传输量，[PCI-E](https://zh.wikipedia.org/zh-cn/PCI_Express) 总线带宽的计算需考虑编码方式、单双工模式何通道数等

$$ 带宽 = \frac{位宽 \times 工作频率}{8} $$

存储器容量：内存(主存)、外存(辅存容量)

![demo](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200226102903.jpg)
