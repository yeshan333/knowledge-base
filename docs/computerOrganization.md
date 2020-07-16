# 计算机组成原理基础

![计算机](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200216204537.png)

## 定理&规律

- 摩尔定律
- 局部性原理
  - 时间局部性
  - 空间局部性

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
  - CPU 倍频：CPU内部用来加速工作效能的一个倍数，CPU 与系统总线相差的倍数，$ CPU 主频 = CPU 外频 \times CPU 倍频 $
  - IPS(Instruction Per Second)：每秒执行指令数
  - CPI(Clock-cycle Per Instruction)：指令平均周期，执行一条指令所需要的时钟周期
  - [FLOPS](https://zh.wikipedia.org/zh-cn/%E6%AF%8F%E7%A7%92%E6%B5%AE%E9%BB%9E%E9%81%8B%E7%AE%97%E6%AC%A1%E6%95%B8)(floating-point operations per second)：每秒浮点运算速度

数据传输率：
  - [带宽](https://zh.wikipedia.org/wiki/%E5%B8%A6%E5%AE%BD)(Bandwidth)，单位时间数据的传输量，[PCI-E](https://zh.wikipedia.org/zh-cn/PCI_Express) 总线带宽的计算需考虑编码方式、单双工模式何通道数等

$$ 带宽 = \frac{位宽 \times 工作频率}{8} $$

存储器容量：内存(主存)、外存(辅存容量)

![demo](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200226102903.jpg)

## 处理器

### CPU 抽象逻辑图

![CPU 抽象逻辑图](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/try20200309160137.png)

### CPU 浅解

![](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/try20200309150658.png)

Fetch(取指令)：PC 寄存器与指令寄存器从内存获取指令

Decode(指令译码)：由控制器（Control Unit）操作

Execute(指令执行)：由算术逻辑单元（ALU）操作

?>所有 CPU 支持的指令，都会在控制器里面，被解析成不同的输出信号。

?>[控制器](https://baike.baidu.com/item/%E6%8E%A7%E5%88%B6%E5%99%A8)由指令寄存器IR（InstructionRegister）、程序计数器PC（ProgramCounter）和操作控制器0C（OperationController）三个部件组成

!>CPU 取指令过后，将指令（一个由0，1构成的字符串）输入译码电路，译码电路根据指令集的描述，生成各种控制信号。**指令集可以看作是 CPU 行为的描述，而 CPU 里面的电路是指令集的实现**。指令集不会被“存储”在某处

#### CPI-指令周期

![CPI-指令周期](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/try20200309151603.png)

?>时钟周期也称为振荡周期，定义为时钟频率的倒数。时钟周期是计算机中最基本的、最小的时间单位。

!>对于现代 CPU，随着流水线设计的引入，一个指令被拆分为多个子流程。一个CPU的时钟时间，应该是这多个子流程中最长的那条的耗时时间

### 无状态电路元件-ALU

>组合逻辑电路（Combinational Logic Circuit）: 给定输入，就能得到固定的输出。

#### 加法器与乘法器

常见门电路表示

![常见门电路](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/img/20200309142214.png)

##### 加法器

加法：二进制竖式运算

![二进制竖式计算](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/img/20200309142549.png)

**半加器电路**

![半加器电路](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/img/20200309142750.png)

**全加器电路：两个半加器 + 或门**

![全加器电路](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/new/20200309144027.png)

**由 8 个全加器组成的 8 位加法器**

![8 位加法器](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/new/20200309143727.png)

##### 乘法器

乘法：二进制竖式运算，**移位 + 加法**

![乘法：二进制竖式运算](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/new/20200309144427.png)

### 有状态电路元件-寄存器

>时序逻辑电路（Sequential Logic Circuit）: 解决“自动”运行、存储与时序协调问题

https://time.geekbang.org/column/article/99092

反馈电路与时钟信号、存储与 D 型触发器

## 存储与IO系统

![存储器层次关系](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/img/20200304092527.png)

![形象比喻](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/img/20200304092858.png)

### 三级缓存

#### CPU的缓存更新策略

##### Cache 写入策略

**写直达(write-through)**：每一次数据都要写入到主内存里面，性能就会受限于内存的访问速度。

**写回(write-back)**：脏数据，即某个时候我们的 CPU Cache 里面的这个 Block 的数据，和主内存是不一致的。

![缓存更新策略](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200716175151.png)

#### 缓存一致性与MESI协议

如图，缓存一致性问题：CPU1核心1 更新数据到自己的 Cache，但没更新到主内存（因为 Write Back 策略，CPU核心1 先把 Cache Block 标记为脏数据，1 号核心希望这个 Cache Block 要被交换出去的时候，才将数据写入主内存），这时 CPU核心2 如果读取数据，读取到的将是脏数据。

![多核CPU缓存一致性问题](https://cdn.jsdelivr.net/gh/ssmath/picgo-pic/img/20200716181451.png)

缓存一致性问题解决机制需满足的条件：
- 写传播：在一个 CPU 核心的 Cache 数据更新必须能后传播到其他相应节点的 Cache Line（缓存地址） 里
- 事务串行化：在一个 CPU 核心里的读取和写入，在其他节点看起来顺序是一样的

**解决方案**

总线嗅探（Bus Snooping），基于总线嗅探机制的 [MESI](https://zh.wikipedia.org/zh-hans/MESI%E5%8D%8F%E8%AE%AE) 协议

> MESI 协议，是一种叫作写失效（Write Invalidate）的协议。在写失效协议里，只有一个 CPU 核心负责写入数据，其他的核心，只是同步读取到这个写入。在这个 CPU 核心写入 Cache 之后，它会去广播一个“失效”请求告诉所有其他的 CPU 核心。


### 内存

#### 虚拟内存到物理内存的多级页表

#### 虚拟内存到物理内存转换的性能提速

地址变换高速缓冲（TLB,Translation-Lookaside Buffer）

#### 内存保护策略

wikipedia：[https://zh.wikipedia.org/wiki/記憶體保護](https://zh.wikipedia.org/wiki/%E8%A8%98%E6%86%B6%E9%AB%94%E4%BF%9D%E8%AD%B7)

**可执行空间保护**

**地址空间部署随机化**

### 设备通信的线路-总线

>事件总线知多少：https://cloud.tencent.com/developer/article/1018409

大型系统开发的设计模式-事件总线(Event Bus)

![Event-Bus-image](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/img/20200304101102.jpg)

#### 多总线架构

CPU 与内存以及高速缓存通信的总线：
- 本地总线（也叫后端总线([Back-side Bus](https://en.wikipedia.org/wiki/Back-side_bus))，）：CPU 与 Cache 通信
- [前端总线](https://zh.wikipedia.org/wiki/%E5%89%8D%E7%AB%AF%E6%80%BB%E7%BA%BF)(Front-side Bus)：CPU 与[北桥芯片](https://zh.wikipedia.org/zh-hans/%E5%8C%97%E6%A1%A5)通信
北桥芯片拆分的前端总线：
- 内存总线（Memory Bus）
- 系统总线（System Bus）

![CPU 硬件架构图](https://cdn.jsdelivr.net/gh/ssmath/images-assets-cdn/img/20200304104022.jpg)

CPU 内的内存接口直接和系统总线通信，然后系统总线再接入一个 I/O 桥接器。这个 I/O 桥接器(I/O Bridge)一边接入了内存总线，使得 CPU 和内存通信。另一边接入 I/O 总线，用于连接 I/O 设备。

#### 多设备通信的总线裁决机制

>wikipedia：https://en.wikipedia.org/wiki/Arbiter_(electronics)

#### 现代的Intel-QPI技术

>[快速通道互联](https://zh.wikipedia.org/wiki/%E5%BF%AB%E9%80%9F%E9%80%9A%E9%81%93%E4%BA%92%E8%81%94)（英语：Intel QuickPath Interconnect，缩写：QPI），是一种由英特尔开发并使用的点对点处理器互联架构，用来实现CPU之间的互联。

### 输入输出设备

### SSD、HDD
