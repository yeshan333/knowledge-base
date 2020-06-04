## 软件工程基础

?> [软件工程](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E5%B7%A5%E7%A8%8B)是指应用计算机科学、数学以及管理学等原理，以工程化的原则和方法来解决软件问题的工程，其目的是提高软件生产率、提高软件质量、降低软件成本。

- 软件工程的核心
  - 软件需求（Software requirements）
  - [软件设计](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E8%AE%BE%E8%AE%A1)（Software design）
  - 软件建构（Software construction）
  - [软件测试](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E6%B5%8B%E8%AF%95)（Software test）
  - 软件维护与更新（Software maintenance）
  - 软件构型管理（Software Configuration Management, SCM）
  - 软件工程管理（Software Engineering Management）
  - [软件开发过程](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E8%BF%87%E7%A8%8B)（Software Development Process）
  - 软件工程工具与方法（Software Engineering Tools and methods）
  - 软件质量（Software Quality）
- 软件工程 7 条基本原理[🔗](http://www.inest.cas.cn/kxcb/kxcb_kpyd/kjqy/201406/t20140616_239883.html)
  - 用分阶段的生命周期计划严格管理
  - 坚持进行阶段评审
  - 实现严格的产品控制
  - 采用现代程序设计艺术
  - 结果应能清楚地审查
  - 开发小组的人员应少而精
  - 承认不断改进软件工程实践的必要性

## 软件过程

软件开发所遵循的路线图即为“软件过程”。

### 软件过程能力成熟度模型（CMM）

![CMM模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215173257.png)

[能力成熟度模型集成（CMMI）](https://zh.wikipedia.org/zh-hans/%E8%83%BD%E5%8A%9B%E6%88%90%E7%86%9F%E5%BA%A6%E6%A8%A1%E5%9E%8B%E9%9B%86%E6%88%90)

![CMMI](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215173334.png)

### 软件过程模型

软件过程模型也称**软件开发模型**。它是软件开发全部过程、活动和任务的结构框架。

**典型模型**：瀑布模型（Waterfall Model）、增量模型（Incremental Model）、演化模型（Evolutionary Model）（原型模型（Prototype Model）、螺旋模型（Sprial Model））、喷泉模型（Water Fountain Model）、基于构件的开发模型（Component-based Development Model）和形式化方法模型（Formal Methods Model）等。

#### 瀑布模型

**模型假设**：待开发的系统需求完整、简洁、一致，可先于设计和实现完成之前产生

**特点**：[瀑布模型](https://en.wikipedia.org/wiki/Waterfall_model)以文档驱动，适合软件需求明确的软件项目的模型

![瀑布模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215190708.png)

**V 模型**:

![V模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215191751.png)

#### 增量模型

**模型假设**：需求可分段为一系列增量产品，每一增量可以分别开发

**模型特点**：[增量模型](https://wiki.mbalib.com/wiki/%E5%A2%9E%E9%87%8F%E6%A8%A1%E5%9E%8B)强调每一个增量均发布一个可操作的产品

![增量模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215192657.png)

#### 演化模型

**模型适用情况**：对如软件需求缺乏准确认知，并非所有需求都能预先定义，[🔗](https://baike.baidu.com/item/%E6%BC%94%E5%8C%96%E6%A8%A1%E5%9E%8B)

**原型模型**：探索型原型、实验型原型、演化型原型

![原型模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215195600.png)

**螺旋模型**：[螺旋模型](https://zh.wikipedia.org/wiki/%E8%9E%BA%E6%97%8B%E6%A8%A1%E5%9E%8B) = 瀑布模型 + 演化模型 + **风险分析**

![螺旋模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215195430.png)

#### 喷泉模型

**特点**：[喷泉模型](https://wiki.mbalib.com/wiki/%E5%96%B7%E6%B3%89%E6%A8%A1%E5%9E%8B)以用户需求为动力，以对象为驱动，适合于面向对象得开发方法

![喷泉模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215202233.png)

#### 基于构件的开发模型

**特点**：[基于构件的开发模型](https://en.wikipedia.org/wiki/Component-based_software_engineering)采用预先打包的软件构件开发应用系统，它的本质为演化模型，以迭代的方式构建软件

![基于构件的开发模型](https://cdn.jsdelivr.net/gh/ssmath/mypic/img/20200215202814.png)

**领域工程**的目的是构建[领域模型](https://baike.baidu.com/item/%E9%A2%86%E5%9F%9F%E6%A8%A1%E5%9E%8B)、领域基准体系结构何可复用构件库。

**应用系统工程**的目的是使用可复用构件组装应用系统。

#### 形式化方法模型

[软件形式化方法](https://baike.baidu.com/item/%E8%BD%AF%E4%BB%B6%E5%BD%A2%E5%BC%8F%E5%8C%96%E6%96%B9%E6%B3%95/18551194?fr=aladdin)是指建立在严格数学基础上的软件开发方法。形式化方法模型的主要活动是生成计算机软件形式化的数学规格说明。形式化方法使软件开发人员可以应用严格的数学符号来说明、开发和验证基于计算机的系统。

#### 统一过程(UP)模型

统一过程模型是一种“用例和风险驱动，以架构为中心，迭代并且增量”的开发过程，由 UML 方法和工具支持。[统一软件开发过程🔗](https://zh.wikipedia.org/wiki/%E7%BB%9F%E4%B8%80%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E8%BF%87%E7%A8%8B)

?>[迭代式开发](https://zh.wikipedia.org/wiki/%E8%BF%AD%E4%BB%A3%E5%BC%8F%E5%BC%80%E5%8F%91)也被称作迭代增量式开发或迭代进化式开发，是一种与传统的瀑布式开发相反的软件开发过程，它弥补了传统开发方式中的一些弱点，具有更高的成功率和生产率。**迭代**一般指某版本的生产过程，包括从需求分析到测试完成。**版本**一般指某阶段软件开发的结果，一个可交付使用的产品。

#### 敏捷开发

**总体目标**：通过“尽可能早地、持续地对有价值的软件的交付”使客户满意。

>[敏捷开发](https://zh.wikipedia.org/wiki/%E6%95%8F%E6%8D%B7%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91)（Agile Development）是一种应对快速变化的需求的一种软件开发能力。它们的具体名称、理念、过程、术语都不尽相同，相对于“非敏捷”，更强调程序员团队与业务专家之间的紧密协作、面对面的沟通（认为比书面的文档更有效）、频繁交付新的软件版本、紧凑而自我组织型的团队、能够很好地适应需求变化的代码编写和团队组织方法，也更注重软件开发过程中人的作用。

### 敏捷开发

!> 来源：https://agilemanifesto.org/iso/zhchs/manifesto.html

#### 敏捷软件开发宣言

![敏捷宣言](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200215213033.png)



#### 敏捷软件的十二条原则

![敏捷软件原则](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200215213152.png)

#### 最佳实践

- 验收测试驱动开发（ATDD）
- 敏捷建模
- 敏捷测试
- [持续集成](https://zh.wikipedia.org/wiki/%E6%8C%81%E7%BA%8C%E6%95%B4%E5%90%88)（CI）
- [结对编程](https://zh.wikipedia.org/zh-hans/%E7%BB%93%E5%AF%B9%E7%BC%96%E7%A8%8B)
- [重构](https://zh.wikipedia.org/wiki/%E9%87%8D%E6%9E%84)
- 回顾
- Scrum事件（冲刺计划，每日Scrum，冲刺回顾和回顾）
- 故事驱动的建模
- [测试驱动开发](https://baike.baidu.com/item/%E6%B5%8B%E8%AF%95%E9%A9%B1%E5%8A%A8%E5%BC%80%E5%8F%91)（TDD）
- 时间盒
- 用户故事
- 用户故事映射
- 速度跟踪
- ...

### 软件测试

[软件测试](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E6%B5%8B%E8%AF%95)，软件测试是一种实际输出与预期输出间的审核或者比较过程。

测试目标：保证系统在各种应用场景下的功能是符合设计要求的。

#### 测试实例之用户登录功能测试

!> 参考：[极客时间软件测试 52 讲解](https://time.geekbang.org/column/article/10030)

##### 初级测试用例

- 输入已注册的用户名和正确的密码，验证是否登录成功；
- 输入已注册的用户名和不正确的密码，验证是否登录失败，并且提示信息正确；
- 输入未注册的用户名和任意密码，验证是否登录失败，并且提示信息正确；
- 用户名和密码两者都为空，验证是否登录失败，并且提示信息正确；
- 用户名和密码两者之一为空，验证是否登录失败，并且提示信息正确；
- 如果登录功能启用了验证码功能，在用户名和密码正确的前提下，输入正确的验证码，验证是否登录成功；
- 如果登录功能启用了验证码功能，在用户名和密码正确的前提下，输入错误的验证码，验证是否登录失败，并且提示信息正确。

- 用户名和密码是否大小写敏感；
- 页面上的密码框是否加密显示；
- 后台系统创建的用户第一次登录成功时，是否提示修改密码；
- 忘记用户名和忘记密码的功能是否可用；
- 前端页面是否根据设计要求限制用户名和密码长度；
- 如果登录功能需要验证码，点击验证码图片是否可以更换验证码，更换后的验证码是否可用；
- 刷新页面是否会刷新验证码；如果验证码具有时效性，需要分别验证时效内和时效外验证码的有效性；
- 用户登录成功但是会话超时后，继续操作是否会重定向到用户登录界面；
- 不同级别的用户，比如管理员用户和普通用户，登录系统后的权限是否正确；
- 页面默认焦点是否定位在用户名的输入框中；
- 快捷键 Tab 和 Enter 等，是否可以正常使用。

##### 进阶测试用例

>一个质量过硬的软件系统，除了显式功能性需求以外，其他的非功能性需求即隐式功能性需求也是极其关键的。

**安全性测试**用例包括：

- 用户密码后台存储是否加密；
- 用户密码在网络传输过程中是否加密；
- 密码是否具有有效期，密码有效期到期后，是否提示需要修改密码；
- 不登录的情况下，在浏览器中直接输入登录后的 URL 地址，验证是否会重新定向到用户登录界面；
- 密码输入框是否不支持复制和粘贴；
- 密码输入框内输入的密码是否都可以在页面源码模式下被查看；
- 用户名和密码的输入框中分别输入典型的“SQL 注入攻击”字符串，验证系统的返回页面；
- 用户名和密码的输入框中分别输入典型的“XSS 跨站脚本攻击”字符串，验证系统行为是否被篡改；
- 连续多次登录失败情况下，系统是否会阻止后续的尝试以应对暴力破解；
- 同一用户在同一终端的多种浏览器上登录，验证登录功能的互斥性是否符合设计预期；
- 同一用户先后在多台终端的浏览器上登录，验证登录是否具有互斥性。


**性能压力测试**用例包括:

- 单用户登录的响应时间是否小于 3 秒；
- 单用户登录时，后台请求数量是否过多；
- 高并发场景下用户登录的响应时间是否小于 5 秒；
- 高并发场景下服务端的监控指标是否符合预期；
- 高集合点并发场景下，是否存在资源死锁和不合理的资源等待；
- 长时间大量用户连续登录和登出，服务器端是否存在内存泄漏。

**兼容性测试**用例包括：

- 不同浏览器下，验证登录页面的显示以及功能正确性；
- 相同浏览器的不同版本下，验证登录页面的显示以及功能正确性；
- 不同移动设备终端的不同浏览器下，验证登录页面的显示以及功能正确性；
- 不同分辨率的界面下，验证登录页面的显示以及功能正确性。

#### 黑盒测试之等价类划分

>[黑盒测试](https://zh.wikipedia.org/wiki/%E9%BB%91%E7%9B%92%E6%B5%8B%E8%AF%95)也称为功能测试，在完全**不考虑软件的内部结构和特性**的情况下，测试软件的外部特性。

![例题](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200604194356.png)

![解答01](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200604194444.png)

测试用例设计

![为等价类设计测试用例](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200604194534.png)

![为每一个无效等价类设计测试用例](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200604194636.png)

!> 注意点：为等价类设计测试用例时，要使测试用例**尽可能多的覆盖等价类**；而为无效等价类设计测试用例时，**一个测试用例覆盖一个无效等价类**。

#### 白盒测试之逻辑覆盖测试

[白盒测试](https://zh.wikipedia.org/wiki/%E7%99%BD%E7%9B%92%E6%B5%8B%E8%AF%95)也成为结构测试，根据程序的内部结构和逻辑来设计测试用例，对程序的路径和过程进行测试，检查是否满足设计的需要。

![白盒测试原则](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200215215050.png)

?> **Alpha** 测试由有代表性的最终用户在开发者场所进行，**Beta** 测试在一个或多个最终用户场所执行。

![https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200604200344.png](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200604200344.png)

### ISO/IEC 9126 软件质量模型

> https://zh.wikipedia.org/zh-hans/ISO/IEC_9126

![ISO/IEC 9126 软件质量模型](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200215215743.png)

## 结构化方法

**指导思想**：自顶向下，逐层分解。

**基本原则**：功能的分解与抽象。

### 系统设计之模块化

?> 模块，系统组成的基本单位，特点是可组合、分解和更换。模块化是将一个待开发的软件分解成若干个小的简单部分-模块每个模块可**独立**的进行开发、测试，最后组装成完整的程序，将一个复杂的问题“分而治之”。衡量模块独立程度的标准：**内聚性和耦合性**。

[耦合性](https://zh.wikipedia.org/wiki/%E8%80%A6%E5%90%88%E6%80%A7_(%E8%A8%88%E7%AE%97%E6%A9%9F%E7%A7%91%E5%AD%B8))(Coupling)，也叫耦合度，是对**模块间**关联程度的度量。

![耦合性](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200222141749.png)

[内聚性](https://zh.wikipedia.org/wiki/%E5%85%A7%E8%81%9A%E6%80%A7_(%E8%A8%88%E7%AE%97%E6%A9%9F%E7%A7%91%E5%AD%B8))(Cohesion)。是对一个模块**内部**各个元素彼此结合的紧密程度的度量。

![内聚性](https://mypic-1258313760.cos.ap-guangzhou.myqcloud.com/img/20200222141840.png)

## 面向对象方法

>面向对象(Object-Oriented)=对象(Object)+分类(Classification)+继承(Inheritance)+通过消息的通信(Communication With Messages)

对象：数据属性+操作数据的行为

消息：对象之间进行通信的一种构造

类：对象之上的抽象，对象是类的具体化，是类的实例

继承：父类与子类之间共享数据和方法的机制。子类可继承父类中的属性和方法而不必重新定义

多态：不同对象收到同一消息可以产生完全不同的结果