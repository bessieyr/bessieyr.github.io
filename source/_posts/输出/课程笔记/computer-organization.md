---
title: 计算机组成
date: 2020-05-04 19:14:20
tags: 课程笔记
mathjax: true
---

> **Abstract**
>
> 自学计算机组成与原理，笔记整理自bilibili的[计算机组成原理（哈工大）](https://www.bilibili.com/video/BV1ix41137Eu?from=search&seid=8515848257907690086)视频课程内容

# 第一部分：计算机

# 计算机系统概论

> 自我检测： [【计算机组成原理】中国大学MOOC哈工大课程第一章测试题库](https://blog.csdn.net/weixin_45087775/article/details/104582401?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)，[【计算机网络】中国大学MOOC哈工大国家精品课程第一章习题（补充）](https://blog.csdn.net/weixin_45087775/article/details/104647650)

## 冯 · 诺依曼计算机

<iframe frameborder= "no" border= "0" marginwidth= "0" marginheight= "0" width=100% height=230 src= "https://edrawcloudpubliccn.oss-cn-shenzhen.aliyuncs.com/viewer/self/17395278/share/2020-6-7/1591519991/main.svg"></iframe>

**特点**

1. 五大组成 <span style="color:#aaa">  辅存可以参考U盘，属于I/O设备 </span>
2. 混合存储：instruct & data不加以区分，以同等地位存储，并依靠address访问
3. instruct & data以二进制表示
4. instruct = 操作码（instruct is to do what） + 地址码（操作数所在的地址）
5. 操作数存于内存中的存储程序，存储程序存于存储器中 <br><span style="color:#aaa"> ☆核心特征（具有存储程序的计算机都称为冯·诺依曼计算机）</span>
6. 以运算器为中心 

**改良**

早期的冯 · 诺依曼计算机是以运算器为中心导致运算器过于繁忙，改良后以存储器为中心，实现I/O设备和存储器间直接的数据交换 。

现代计算机采系统复杂性管理方法，用层次化的结构来表述计算机系统的硬件结构，如下图所示：

<span style="color:#aaa"> 實綫：數據通過，虛綫：控制和狀態反饋，双线箭头：数据的传输 </span>

<img src="https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200505154317.png" width="40%"/>

## 主机的基本构成

<iframe frameborder= "no" border= "0" marginwidth= "0" marginheight= "0" width=100% height=400 src= "https://edrawcloudpubliccn.oss-cn-shenzhen.aliyuncs.com/viewer/self/17395278/share/2020-6-7/1591520989/main.svg"></iframe>

**存储容量的计算**

存储字长 = MDR位数

存储体内的单元数 = 2<sup>MAR的位数</sup>

存储体的size = 2<sup>MAR位数</sup>×MDR位数

 ☆【单位转化】B：Byte字节，b：bit位，1字节 = 8位（2<sup>3</sup>b=1B，2<sup>30</sup>B=1GB，1K=2<sup>10</sup>）

**指令流程**

<img src="https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200505154251.png" width="60%"/>

取指令：PC→MAR→M→MDR→IR（把指令从给定的内存单元中取出，放入IR），取完指令后(PC)+1→PC

分析指令：OP(IR)→CU	<span style="color:#aaa">OP表示IR中的操作码，由CU对操作码进行分析</span>

执行指令：Ad(IR)→MAR→M→MDR→ACC	<span style="color:#aaa">Ad：address</span>

## 机器性能指标

| WAYS        | NAME               | INFORMATION                                 |
| ----------- | ------------------ | ------------------------------------------- |
| 1. 机器字长 | 机器字长           | CPU能处理数据的位数                         |
| 2. 运行速度 | 主频               | 机器内部主时钟的频率，是时钟周期的倒数      |
|             | 每个核支持的线程数 |                                             |
|             | 核数               |                                             |
|             | 吉普森法           | $T_{M}=\sum_{i=1}^nf_{i}t_{i}$              |
|             | CPI                | 执行一条指令所需的时钟周期数                |
|             | MIPS               | 每秒执行多少百万条指令                      |
|             | FLOPS              | 每秒浮点运算次数                            |
| 3. 存储容量 | 主存容量           | 表示方法：①存储单元个数 × 存储字长  ②字节数 |
|             | 辅存容量           | 表示方法：字节数                            |

---

<details>
    <summary>Question：MAR为10位，MDR为8位，问该存储体的容量为多少？（请用两种方式表示）</summary>
    <br>∴ ①1K × 8位 ②1KB
</details>


---

# 总线

## 总线的基本概念

<img src="https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200522171637.png" width="40%"/>

意义：连接各部件信息的公共传输线，解决分散连接使散线过多系统难以扩展的问题

由于总线一次只能允许一个部件的使用，<font color="red">单总线结构</font>会造成各部件对总线的争用，因此又衍生出<font color="red">多总线结构</font>。

**总线的信息传送方式**

- 串行：信息一位一位地传输
- 并行：信息多位并行传输 <font color="#aaa">并行方式需要多条数据线进行传输，线与线之间会产生干扰，若传输距离较长，信号会发生变形</font>

## 总线的分类

| WAYS              | CATEGORY | MEANING                                                      |
| ----------------- | -------- | ------------------------------------------------------------ |
| 1. 按位置功能划分 | 片内总线 | 在芯片内部的总线                                             |
|                   | 系统总线 | 位在芯片之外，计算机各部件之间的信息传输线（数据总线+地址总线+控制总线） |
|                   | 通信总线 | 计算机和计算机或其他系统之间的通信线（串行通信总线+并行通信总线） |
| 2. 按传送内容划分 | 数据总线 | 双向传输总线。<font color="blue">位数与机器字长、存储字长有关</font> |
|                   | 地址总线 | 单向传输总线，指出数据所在的地址。<font color="blue">位数与存储单元个数有关</font> |
|                   | 控制总线 | 传输控制信息<br>常见控制信号：时钟（用于同步）、复位（初始化）、总线请求/允许、中断请求/响应、读/写、传输响应（表示数据已被接受） |

| NAME     | INFORMATION                                                  |
| -------- | ------------------------------------------------------------ |
| I/O总线  |                                                              |
| 主存总线 |                                                              |
| DMA总线  | direct memory access直接内存存取，使外部设备可以直接访问系统内存 |
| 局部总线 | 用于 ①cpu和cache高速缓冲区 ②桥的连接                         |
| 扩展总线 | 连接各种外设                                                 |
| 高速总线 | 连接高速设备                                                 |

## 总线特性及性能指标

**性能指标**

| NAME          | INFORMATION                                                  |
| ------------- | ------------------------------------------------------------ |
| 总线宽度      | 总线上能同时传输多少<font color="blue">位数</font>的数据，即<font color="red">数据总线的根数</font> |
| 标准传输率    | 每秒传输的最大字节数（MBps）                                 |
| 总线时钟      | **总线时钟频率**，是总线时钟周期的倒数，表示<font color="blue">每秒</font>可以传输的次数（ex. 8MHz=每秒可传输8兆次）<br>**总线时钟周期**，机器的时钟周期 |
| 总线传输周期  | 一次总线操作所需的时间（<font color="blue">申请+寻址+传数+结束</font>），包含若干个时钟周期。<br>**总线工作频率**是它的倒数 |
| 带宽          | 每单位时间可传输的信息数量<br/><font color="red">带宽 = 总线宽度（每次传输的数据位数）× 总线频率</font> |
| 时钟同步/异步 |                                                              |
| 总线复用      | 地址线与数据线复用                                           |
| 信号线数      | 地址线、数据线、控制线的总和                                 |
| 总线控制方式  | 突发、自动、仲裁、逻辑、计数                                 |
| 其他指标      | 负载能力                                                     |

**常见总线标准**

| 总线标准 | INFORMATION                                                  |
| -------- | ------------------------------------------------------------ |
| ISA      | 工业标准体系结构（带宽16MBps = 数据线16×总线时钟8MHz = 2Byte×8MHz） |
| EISA     | 对ISA的扩展，可兼容ISA卡的使用，数据线宽度32位，传输带宽增加了一倍（<font color="blue">低速总线</font>） |
| VESA     | 视屏电子标准协会。为应对PC要求高速传输的活动图像而出现的总线类型。很多数据来自CPU，驱动能力较差。（<font color="blue">高速总线</font>） |
| PCI      | Peripheral Component Interconnect，外设部件互联标准。是当前计算机用的最多的接口，是独立于处理器的结构，将CPU和外围设备分开，形成中间缓冲器的作用。外面的用户就可以随意添加外围设备，不用担心由于时钟周期的不同，导致系统性能的下降。（高速总线）<br>通过多层PCI桥可实现总线驱动力的提高和总线的扩展 |
| AGP      | 点对点的局部总线，主要用于连接控制芯片和显卡，由PCI发展而成，速度较快最高可达32x133MHz=533MBps |
| RS-232   | 串行通信总线标准                                             |
| USB      | 通用串行接口总线                                             |
| SCSI     | 小型计算机系统接口，用于计算机和智能设备(硬盘、光驱、打印机等）之间系统级接口的独立处理器标准 |
| SATA     | 串行高级技术附件，基于行业标准的串行硬件驱动器接口           |

## 总线控制与通信

目的：解决主从设备之间的协调配合问题

<font color="#aaa">主设备/模块：对总线有控制权，从设备/模块：要听从响应从主设备发来的总线控制命令</font>

<iframe frameborder= "no" border= "0" marginwidth= "0" marginheight= "0" width=100% height=400 src= "https://edrawcloudpubliccn.oss-cn-shenzhen.aliyuncs.com/viewer/self/17395278/share/2020-6-7/1591467698/main.svg"></iframe>

**总线控制**

| 链式查询                                                     | 计时器定时查询                                               | 独立请求                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200606174006.png) | ![](https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200606174022.png) | ![](https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200606174017.png) |

**总线通信**


| 同步通信                                                     | 异步通信                                                     | 半同步通信                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![](https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200522174819.png) | ![](https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200522174848.png) | ![](https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200522175002.png) |

| **总线传输周期**                                     | **同/异/半同步通信的一个总线传输周期**                       | **分离式通信的一个总线传输周期**                             |
| ---------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 1. 申请分配阶段：主设备获得总线的使用权              | 1. 主模块发出地址和命令，总线被占用                          | 1. 主模块申请占用总线，使用完后，立即放弃总线使用权          |
| 2. 寻址阶段：主设备发出地址找到从设备                | 2. 从模块准备数据，并不占用总线，总线处于被主模块仍旧占用的空闲状态 | 2. 上一步骤结束后，从设备准备即将发出的数据，若已准备好，则申请占用总线，成为主模块，将各种信息送至总线上 |
| 3. 传数阶段：从设备在准备就绪的情况下，发送/接受数据 | 3. 从模块向主模块发送数据，总线不再空闲。                    |                                                              |
| 4. 结束阶段：主模块与从模块撤销相关信息              |                                                              |                                                              |

# 存储系统

**存储器<font color="blue">（按照存储介质分类）</font>**

- 半导体存储器：按照01输入，来表示高低电频（ex.计算机的内存芯片、u盘）
- 磁表面存储器：靠磁头读出、写入
- 光盘存储器：利用光烧制，利用光写出

**存储器<font color="blue">（依照作用功能分类）</font>**

- 主存储器（半导体存储器）
  - RAM：SRAM+DRAM
  - ROM：MROM+PROM+EPROM+EEPROM
- Flash Memory：可作为便携式存储器（ex.U-disk），也可作为计算机的硬盘，它是SSD的核心材料<font color="#aaa">SSD全名Solid-state drive固态硬盘</font>
- 高速缓冲存储器（Cache）
- 辅助存储器

**存储器的层次结构**

<font color="#aaa">对存储体+MDR+MAR的这种主存结构进行了更细部的划分说明</font>

<img src="https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200522175004.png" width=50%/>

![](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200525211923534.png)

- 不同存储层次结构的搭配，使对程序员来说这个整体拥有主存的容量、缓存的速度和价格。
- <font color="red">缓存-主存层次</font>主要是为了解决CPU和主存间<font color="blue">速度</font>不匹配问题，因此用硬件来做。所使用地址就是主存储器的地址。<font color="#aaa">缓存是靠内容进行查找，即是给出了地址也只是个编号。</font>
- <font color="red">主存-辅存层次</font>主要是为了解决<font color="blue">容量</font>问题，采软硬件相结合。其构成的成体称为”虚拟存储器“，匹对的地址为虚地址。

## 主存储器

<iframe frameborder= "no" border= "0" marginwidth= "0" marginheight= "0" width=100% height=860 src= "https://edrawcloudpubliccn.oss-cn-shenzhen.aliyuncs.com/viewer/self/17395278/share/2020-6-16/1592239820/main.svg"></iframe>

**半导体存储芯片**

<img src="https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200522175007.png" width=50%/>

| NAME         | INFORMATION                                                  |
| ------------ | ------------------------------------------------------------ |
| 译码器       | 对要访问的存储单元地址进行译码，译码之后才能选定指定的存储单元 |
|              | 将地址线传输来的二进制数据转换成对应的存储器单元编号，再辅以控制信号，就可以寻找到对应地址进行驱动。 |
| 读写控制电路 | 控制读写的方向。<br><font color="#aaa">若是写入，就将MDR的数据送到MAR指定的存储体地址中。若是读出，则存储体中指定的数据就会被送到MDR中读出。</font> |
| 片选线       | 给指定的地址，提供一组有效的芯片选择                         |

**RAM：<a href="/2020/06/07/RandomAccessMemory/" target="_blank">Random Access Memory详细说明</a>**

**寻址**

| **主存**<br>（该主存地址线为24位） | ![image-20200616005328163](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616005328163.png) | ![image-20200616005401497](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616005401497.png) |
| :--------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|              **字长**              |                      4位的16进制 = 32位                      |                      2位的16进制 = 8位                       |
|        **按字节寻址的范围**        |                     2<sup>24</sup> = 16M                     |                             16M                              |
|         **按字寻址的范围**         |                    2<sup>24</sup>/4 = 4M                     |                    2<sup>24</sup>/2 = 4M                     |

<font color="#aaa"><b>∵</b>主存是按字节编址	<b>∴</b>地址的范围=按字节寻址的范围</font>

**技术指标**

- 存储容量
- 存储速度：通过<font color="red">存取时间</font>、<font color="red">存取周期</font>、<font color="red">存取带宽</font>来判断

| NAME                          | INFORMATION                                                  |
| ----------------------------- | ------------------------------------------------------------ |
| 存取时间                      | 存储器的访问时间（读出时间、写入时间）                       |
| <p id="存取周期">存取周期</p> | <font color="blue">连续</font>两次<font color="blue">独立</font>的存储器操作所需要的<font color="blue">最小间隔时间</font><br/><font color="#aaa">一般来说存取周期要比存取时间长，周期=找地址时间+存取时间+复原时间</font> |
| 存储带宽                      | 单位时间能向存储器写入/读取多少位的数据（单位：位/秒）       |

---

<details>
    <summary>Question<br>&emsp;若有地址线（单向）14根，数据线4根，请问该芯片的容量为多少？（用nK × n位表示)</summary>
	<br>&emsp;ANS: MAR=14，MDR=4，主存容量为16K × 4位。 <font color="red">不会的话请回看计算机系统概论中“主机的基本构成”和“机器性能指标”部分</font>
</details>

<details>
    <summary>Question2<br>&emsp;假设有n根输入线，译码驱动方式分别采用线选法和重合法，则输出线的数量分别会是多少？</summary>
	<br>&emsp;ANS: 线选法为2<sup>n</sup>，重合法为2<sup>n/2</sup>×2 = 2<sup>1+n/2</sup></font>
</details>


---

<font color = "red">请自行阅读并完成《计算机组成原理》例4.1、4.2以掌握：  </font>

1. 如何根据主存地址空间的分配范围计算出容量
2. 如何选择存储芯片
3. 如何画cpu与存储芯片连接逻辑图（数据线、地址线、读写控制线的连接）
4. 课本可能有点难啃，但了解清楚后就会觉得很多东西都豁然开朗了，称赞下自己是个小天才叭ヽ( ’ ω ’  )ノ！

## 存储器的校验（海明码）

**纠错理论**

| NAME           | INFORMATION                                                  |
| -------------- | ------------------------------------------------------------ |
| 编码的最小距离 | 任意两组代码之间二进制位数的最少差异。 <br>ex. {000,010,001,100,110,111,101}最小距离=1，{000,011,101,110}最小距离=2，{0000,1111}最小距离=4 |

编码的检错、纠错能力和编码的最小距离有关：<font color="red">L-1 = D+C（D≥C）</font>

L：length 编码的最小距离，D：detection 检错的位数，C：correction 纠错的位数

**海明码**

采用奇偶校验+分组校验（非划分）

- 奇偶校验：添加1位1 or 0的校验位，使序列满足校验需求的奇偶性。以判断该序列是否有错
  - 奇校验：让原有数据序列中（包括要加上的一位校验位）1的个数为奇数
  - 偶校验：让原有数据序列中（包括要加上的一位校验位）1的个数为偶数

- 非划分的分组校验：组和组之间有重叠 ，以判断出错的位置 <font color="#aaa">//若有错，基本就错1位</font>

  ​	P1 P2 P3 = 000，表示组1组2组3都无差错

  ​	P1 P2 P3 = 001，表示组3 - 组3∪组2 - 组3∪组1的部分有错

  ​	P1 P2 P3 = 011，表示组2 ∩ 组3有错


信息位n和校验位k应满足：<font color="red">2<sup>k</sup> ≥ n+k+1</font> <font color = "#aaa">//检测结果需要指出这n+k位是哪一位错，还有1位是没有错，所以总状态数为n+k+1，这些状态我们是用k位的2进制数进行编码 ex. xxx1,xx1x,x1xx,1xxx</font>

<font color="red">海明码部分的详情内容建议自行参阅《计算机组成原理》</font>

---

<details>
    <summary>Quiz1：分别求出按配偶原则和配偶原则配置0011的汉明码</summary>
    &emsp;ANS：1000011，0101011
</details>

<details>
    <summary>Quiz2：若已知接受到的汉明码为0100111（按配偶原则配置），试问要求传送的信息是什么？</summary>
    &emsp;ANS：0101
</details>

<details>
    <summary>Quiz3：写出按偶校验配置的汉明码0101101的纠错过程</summary>
    &emsp;ANS：P4P2P1=100，第4位错，可不纠。
</details>


---

## 提高访存速度的措施

存储器的速度 < CPU的速度，但CPU的数据、指令以及保存运行结果都需要依赖到内存，造成了“存储墙”的影响，为了解决该问题，可采用措施：

1. 采用高速器件
2. 采用层次结构：Cache-主存（Cache是由静态RAM做的，速度快，集成度低，功耗大）
3. 调整主存结构

**高性能存储芯片**

- SDRAM（同步DRAM）
- RDRAM
- 带Cache的DRAM

**调整主存结构**

- 单体多字

  存储体中包含多个机器字，以提高带宽。

  详细说明：一个存储体中包含了4个机器字，每1个机器字都是1条机器指令。cpu每次访问，就会将这4个值一起放入ACC中，下次再使用时就可以直接从数据寄存器中取出数据。从而，带宽提高了4倍→每隔1/4个存取周期就可以执行1条指令。

  Cons：4个机器字是以整体的方式进行存取，若遇到转移指令或操作数不连续的情况，会造成4条指令中只有1条有用其余无用的浪费。<br>![image-20200604151600875](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200604151600875.png)

多体并行

- 高位交叉

  编址格式：体号（前两位）+体内地址（后四位）。体号决定存储体，体内地址决定存储体内的存储单元。可同时访问不同的体，实现并行。

  编址顺序：依<font color = "blue">顺序编址</font>，即竖向编址。

  Pros：由于体内的地址是连续的，有利于存储器的扩充。

  Cons：按照程序、数据连续存取的特征，会造成某一个存储体特别繁忙（正所谓一体有难，三体点赞٩(๑òωó๑)۶）

- 低位交叉

  编址格式：体内地址（前四位）+体号（后两位）

  编址顺序：<font color = "blue">各个体轮流进行编址</font>，即横向编址。

  features：在不改变存取周期的前提下，增加存储器带宽。一个存取周期内会以流水线方式来轮流访问不同的存储体，一次总线操作启动一个存储体。

---

<details>
    <summary>Question：设四体低位交叉存储器，存取周期为T，总线传输周期为τ，为实现流水线的方式存取，问T和τ应满足什么样的关系？若需要连续读4个字需要多长时间？若该存储器为高位交叉存储器，连续读4个字又需要多久？</summary>
    <br>&emsp;ANS：T=4τ，低位交叉存储器连续读4个字的时间为T+(4-1)τ，高位交叉的时间为4T<br>
    <img src="https://raw.githubusercontent.com/bessieyr/asset/master/img/20200604192853.png" width="50%"/>
    <div align="center" style="color:#aaa; font-size:14px">低位交叉存储器流水线工作方式示意图</div>
</details>


---

## 高速缓冲存储器

目的：作为主存和CPU间的缓冲，容量小速度快

主存：块号+块内地址

Cache：标记（记录主存的块号，用以CPU判定该块是否有被命中至Cache中）+块号+块内地址

Cache命中率，跟容量和块长有关

效率$e=\frac{\text{访问cache时间}}{\text{平均访问时间}}\cdot100\%$

令访问cache时间为t<sub>c</sub>，访问主存时间为t<sub>m</sub>，命中率为h，则$e=\frac{tc}{ht_{c}+(1-h)t_{m}}$，效率范围为$\frac{t_{c}}{t_{m}}\sim 1$

**Cache的基本结构**

![image-20200605113531942](https://cdn.jsdelivr.net/gh/bessieyr/asset/img/20200605172137.png)

| NAME                      | INFORMATION                                                  |
| ------------------------- | ------------------------------------------------------------ |
| 主存Cache地址映射变换机构 | 映射用于寻找哪个标记可以存入块号，变换用于寻找哪个标记拥有该块号 |
| Cache替换机构             |                                                              |

Cache的读写操作

写操作需要满足数据的一支

write through直写法：始终保持CPU和存储的一至，可能会造成重复写入

write after：退出缓存时再写入CPU



Cache的改进

增加级数

分开存储 for 流水 or 统一存储 地址+指令



映射

直接相联映射：1个主存块只能映射到固定的1个Cache块中。内存按Cache的大小分区，区号写入Cache的标记中。Cache利用率低、速度块

全相联映射：1个主存快可映射至任意1个Cache块中。成本高，Cache利用率高，速度慢。

组相联映射：1个主存快能映射至固定Cache组中的任意1块。折中。



替换算法

先进先出算法（FIFO：first in first out）

近期最少使用算法（LRU：last resently used）



## 辅助存储器

非重点，os考，计组不考

磁盘，磁头：磁盘旋转，给定的磁道旋转到磁头下方，磁头开始读写数据

记录密度

- 道密度：径向上有多少单位磁道D<sub>t</sub>
- 位密度：单位磁道上保存了多少的二进制信息D<sub>b</sub>

数据传输率D<sub>r</sub>=D<sub>b</sub>×V位密度和旋转速度

# 输入输出系统

早期

- 分散连接
- CPU和I/O设备串行：程序查询方式 //I/O设备输入输出时，CPU必须运行相应的程序或停滞等待状态

接口模块和DMA阶段（DMA：Direct Memory Access）

- 总线连接
- 并行：
  - 中断方式
  - DMA方式

通道结构阶段（类似于小型的功能更强的DMA控制器）

- 拥有自己的通道程序，通过执行通道程序来控制连接于通道的I/O设备，和主机直接进行数据传输

I/O处理机

- 数据传输独立性更强

组成

- I/O指令
  - 操作码（I/O标志）+命令码（CPU的操作码）+（I/O设备orI/O寄存器又称I/O端口的地址）
- 通道指令
  - 指出数组首地址、传送字数、操作命令

I/O设备与主机的联系（编址--选址--传送--联络--连接）

1. 编址方式

	- 统一编址，用取数存数指令
	- 不统一编址，用专门的I/O指令
2. 联络方式
   1. 立即响应
   2. 异步响应
3. 连接方式
   1. 辐射式（即发散式）：主机接多个外设，增加I/O就需要增加一套控制电路，每台设备都配有一套控制线路，和一组信号线，不便于增删设备
   2. 总线连接

I/O设备与主机信息传送的控制方式

1. 程序查询方式<br>![image-20200611220134737](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200611220134737.png)<br>CPU会反复等待I/O准备完毕，CPU和I/O串行

2. 程序中断方式

   - I/O工作处于准备期时，CPU不查询，直到需要主机交换信息，外部设备才会主动发出中断现行程序请求。![image-20200611221242907](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200611221242907.png)

3. DMA方式

   - 主存和I/O间有一条直接的数据通道，周期挪用（窃取）来实现I/O与主存间的传送

   - dma方式的存取周期中cpu虽然无法访问内存，不能使用总线，但仍可以执行处理运算。
   - 无需保存现场、恢复现场，无需执行中断程序，无需用软件完成数据的输入和输出

4. 比较：I/O系统的自治能力越来越强<br>![image-20200611224348606](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200611224348606.png)

用总线对主机和外部设备进行连接

## I/O接口

接口的功能

- 实现设备的选择（设备选择线，传送设备/端口的地址，在I/O接口进行匹配，单向线，看是否是对应的接口-设备选择电路）
- 数据缓冲以达到速度匹配
- 数据串-并格式转换
- 电平转换
- 传送控制命令（命令线-命令寄存器、命令译码器）
- 反应设备状态（状态线-设备状态标记=完成触发器D+工作触发器B+中断请求触发器INTR+屏蔽触发器MASK）<br>屏蔽触发器：看当前主机工作的重要性判断是否发出中断请求
- （数据线：输入输出-数据缓冲寄存器）

![image-20200612104601880](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612104601880.png)

![image-20200612105045864](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612105045864.png)

DBR：data buffer register

接口类型（分类）

- 传送方式：并行接口、串行
- 功能选择的灵活性：可编程接口、不可编程
- 按通用性：通用接口、专用接口
- 按数据传送的控制方式：中断接口、DMA接口//程序查询不需接口

## 程序查询方式

接口电路：

![image-20200612114654731](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612114654731.png)

## 程序中断方式

![image-20200612115134568](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612115134568.png)

中断方式的接口电路

- 配置中断请求触发器和中断屏蔽触发器
  - INTR（interrupt）中断请求触发器：INTR = 1有请求
  - MASK中断屏蔽触发器：MATK = 1被屏蔽
  - ![image-20200612120340624](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612120340624.png)
  - 
- 排队器
  - 硬件的排队电路放置位置 => 链式排队器（菊花链？？？？）
    1. 集中放在CPU内部
    2. 放在每一个接口电路中，组成一个链
  - 软件方式进行排队，通过查询的方法，从高优先级到低优先级进行查询的过程（后续第八章介绍）
  - ![image-20200612121121845](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612121121845.png)
    - 优先级：INTR1>INTR2>INTR3>INTR4
    - ​	当没有中断请求时，输出'是1
    - 当设备有中断请求INTR=1，$\overline{INTR}$=0，INTR'=0，其余之后的输出’都会是0
    - 紫线=0，黄线=1
    - 硬件设计的基本器件是与非门，不使用与门
  - ![image-20200612123520816](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612123520816.png)
    - 这样就只有有中断请求的输出会是1
    - 
- 中断向量地址
  - 入口地址
    - 由软件产生：第八章
    - 硬件向量法：由硬件产生向量地址（排队器输出得到），在有向量地址找到入口地址
    - ![image-20200613112713210](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200613112713210.png)
    - 
- 程序中断方式接口电路的组成
  - ![image-20200612125600811](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200612125600811.png)
- I/O中断处理过程
  - CPU响应中断条件：允许中断触发器EINT=1
  - 响应的时间：当D=1，MASK=0（允许接口提出中断服务请求），在每条指令执行阶段的结束前，CPU发中断查询信号（将EINT=1）
  - ![image-20200613114655941](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200613114655941.png)
- 中断服务程序的流程
  1. 保护现场
     1. 程序断点的保护：中断隐指令，硬件要自行完成操作，并非一条真的指令，在第九章
     2. 寄存器内存的保护：进桟指令，因为中断返回后，主程序可能好需要这些值进行操作
  2. 中断服务
  3. 恢复现场：出栈指令
  4. 中断返回：中断返回指令
- 单重和多重中断
  - 单重
  - 多重：允许更高优先级中断原本的中断（套娃！）
  - ![image-20200613115826351](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200613115826351.png)
- 主程序和服务程序抢占CPU
  - ![image-20200613120308624](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200613120308624.png)
  - 宏观上CPU和I/O并行工作
  - 微观上CPU中断现行程序

##　ＤＭＡ方式

- DMA程序和程序中断，DMA无需经过CPU
  
  - ![image-20200613123405259](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200613123405259.png)
  
- DMA与主存交换数据的方式
  1. 直接停止CPU访问主存
  2. 周期（内存访问周期）挪用/窃取
     - DMA占用一个或几个周期完成数据传输，在数据传输间隔DMA放弃对总线的占用
     - CPU不妨问主存->访存使用权直接配给DMA
     - CPU正在访存->DMA不访存
     - CPU和DMA同时请求访存->DMA优先因DMA上连接的是高速设备，若不响应，可能造成数据流失
  3. 交替访问
  
- DMA接口功能

  1. 向CPU申请DMA传送
  2. 处理总线控制权的转交
  3. 管理系统总线、控制数据传送
  4. 确定数据传送的首地址和长度，修正传送过程中数据地址和长度
  5. DMA传送结束时，给出操作完成信号

- DMA接口组成

  - ![image-20200614091644746](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614091644746.png)
  - AR：Address//储存对应存放的内存位置
  -  WC：Word Counter//每传输一组数据+1
  - DAR：Device Address Register（设备地址寄存器，供设备电路选择使用表达是否存在这个DMA接口，可以保存各种编号用来表示传输数据的地址）
  - BR：Buffer（即DBR）
  - DREQ：device request
  - DACK+HLDA应答信号，HLDA是总线的应答

- DMA工作过程

  - ![image-20200614094732506](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614094732506.png)

  - DMA传送过程

    1. 预处理：预置如下信息
       - 通知DMA控制逻辑传送方向入or出
       - 设备地址->DAR
       - 主存地址->AR
       - 传送字数->WC
    2. 数据传输过程
       - ![image-20200614095001260](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614095001260.png)
    3. 后处理
       - 检验送入主存的数是否正确
       - 是否继续用DMA
       - 测试传送过程是否正确，错则转诊断程序
       - <font color="blue">由中断服务程序完成</font>

  - DMA接口与系统的连接方式

    - 具有公共请求线的DMA请求，类似链式
    - 独立的DMA接口，类似独立请求

  - DMA方式与程序中断方式的比较

  - |              | 中断方式                    | DMA方式      |
    | ------------ | --------------------------- | ------------ |
    | 数据传送     | 由中断程序完成，需要CPU参与 | 硬件         |
    | 响应时间     | 指令执行结束                | 存取周期结束 |
    | 处理异常情况 | 能                          | 不能         |
    | 中断请求     | 为了传送数据                | 为了后处理   |
    | 优先级       | 低                          | 高           |

- DMA接口类型

  - 选择型：有多个设备连接，但CPU运行到输入输出指令到数据准备以及数据传输都只有一个设备运行
  - 多路型：数据准备阶段可以多个设备并行准备，但数据传输时也只能有一个设备和内存进行传输
    - ![image-20200614101702231](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614101702231.png)

# 第二部分：CPU-ALU

# 运算

主要了解ALU的计算方式

## 无符号数和有符号数的表示

**原码**表示法

- 整数 //-2<sup>n</sup>＜x＜2<sup>n</sup>  //逗号分隔数值与符号

  - x = +1110 → [x]<sub>原</sub> = 0,1110
  - x = -1110 → [x]<sub>原</sub> = 2<sup>4</sup>+1110 = 1,1110

- 小数 //-1 < x < 1 //小数点分隔符号与数值

  - x = +0.1100 → [x]<sub>原</sub> = 0.1100
  - x = -0.1100 → [x]<sub>原</sub> = 1.1100

- <details>
      <summary>question：求x = 0的原码</summary><br>
  	&emsp;ANS：假设机器数的数值长度是4位，x = 0时可以用正数、负数、整数、小数的表示。	
      <br>&emsp;&emsp;&emsp;&emsp;[x]<sub>原</sub>: ①[+0]<sub>原</sub> = 0.0000 ②[-0]<sub>原</sub> = 1.0000 ③[+0.0000]<sub>原</sub> = 0,0000 ④[-0.0000]<sub>原</sub> = 1,0000
  </details>

**补数**：用于将减法能转换成加法计算

- 补数的基本概念

  - ![image-20200614134424689](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614134424689.png)
    - 记作1011&equiv;0101（mod 2<sup>4</sup>）//负数与补数相加=模，这里的模是2<sup>4</sup>
    - -0.1001&equiv;1.0111 (mod 2)

- 正数的补码：最大值就是2<sup>n</sup>-1，所以会得到如下范围定义，最小可表示到-2<sup>n</sup>，同时+0和-0的补码表示相同，2<sup>n</sup>和-2<sup>n</sup>相同

  - ![image-20200614163457164](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614163457164.png)
  - 正数的补数即本身
    - ![image-20200614135608956](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614135608956.png)

  - 由于一个数的补数可能是它本身，也可能是负数，因此再加上一位的模来表示正负，逗号分隔补数的符号位
    - ![image-20200614140056002](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614140056002.png)

- 小数补码：范围(1, -1]，mod为2

  - ![image-20200614153642969](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614153642969.png)
  - mod 4小数前有两位，mod 8有3位

- 补数的快捷方式：真值为负值时，补码除了符号位取1，其余每位取反，末位加一（<font color="red">取反加一</font>）

  - ![image-20200614154149704](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614154149704.png)<br>![image-20200615152637333](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615152637333.png)
  - <font color="red">补码转换原码可以用补数的补数的思路！！！</font>符号位变一下就可得到真值！！！太酷了这个！！！

- 练习

- ![image-20200614160528750](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614160528750.png)

  - 70=2<sup>6</sup>+2<sup>2</sup>+2=1000110
  - 答案： 
    - 0,1000110 //<font color="red">注意正值符号位的0！！</font>
    - 1,011010
    - 0.1110
    - 1.0010
    - 0.0000 
    - 0.0000 //<font color="red">由于补码得到的10.0000前面的1会溢出不见，所以在-0.0000的补码上会跟0.0000相同，但是如果是原码则会不同，-0.0000的原码是1.0000</font>
    - 1.0000 //<font color="red">-1.0000在小数补码的(1, -1]的区间内有补码，但无原码！！</font>

**反码**：用是除符号位外，单纯的取反

- ![image-20200614171626870](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614171626870.png)
- ![image-20200614171705732](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614171705732.png)
  - 2<sup>-n</sup>就是最后那个加一，由于不做，所以要反向扣回来！
- [0.0000]<sub>反</sub>=0.0000，[-0.0000]<sub>反</sub>=1.1111
- ![image-20200614172901548](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614172901548.png)
- <font color="red">[y]<sub>补</sub>→[-y]<sub>补</sub>：连同符号位在内，每位取反末位加1（[y]<sub>补</sub>→[-y]<sub>补</sub>就是补数+正值不变的过程）</font>

**移码**：<font color="red">只有整数形式的定义！因用于浮点数据表示的接码部分。</font>能比补码等更直观地直接比较其真值的大小。-2<sup>n<sup>的补码是n+1个符号位的1因此存在！

- ![image-20200614174629745](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614174629745.png)
- 移码和补码的符号位刚好相反，其他都一样
- ![image-20200614175253624](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614175253624.png)

## 定点与浮点表示

**定点**

- ![image-20200614180249796](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200614180249796.png)

**浮点数**

- N=S×r<sup>j</sup>，S：尾数，r：尾数的基值，j：阶码

- 计算机中尾数的值均是≤1

- ![image-20200615124310665](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615124310665.png)

- ![image-20200615124848099](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615124848099.png)

- ![image-20200615125736099](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615125736099.png)

  - s<sup>m</sup>-1类比科学记数法，正值扩张，负值缩小。1-2<sup>-n</sup>代表小数范围

- <details>
      <summary>Question：设机器字长为24位，欲表示±3万的十进制数，在保证数的最大精度的前提下，除阶符数符各一位外，阶码、尾码各取几位？</summary>
      <br>&emsp;&emsp;ANS：<img src="C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615133328176.png"/>
  </details>

- 浮点数规格化

  - ![image-20200615133835530](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615133835530.png)
  - 证明上方结论<br>![image-20200615134359639](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615134359639.png)

- 课本例题

  - ![image-20200615143014202](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615143014202.png)

- 机器零

  - 当阶码为零或者位数为零时，机器“判0”，比如在浮点机中就会表示为：0,0000；0.00...00

## 定点运算

**移位运算**

- 意义：移动<font color="blue">相对于符号位</font>的位置
- 移位原则<br>![image-20200615152812280](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615152812280.png)
- 例题
  - ![image-20200615153803265](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615153803265.png)
  - ![image-20200615162857845](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615162857845.png)
- 实现移位的硬件电路
  - ![image-20200615162407535](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615162407535.png)
    - 真值为正时符号位不变，构成一个循环，左移最高位丢掉 那个向下的箭头就是丢弃的意思，最低位补0 把0用箭头给它，其他类似
    - 这里的丢1是指真值、原码、补码等一律丢的都是1，如果丢的对应真值是0就不会出错
- 逻辑位移：不存在符号数，整体移动，而算数位移存在不动的符号位

**加减运算**

- 算法
  
  - ![image-20200615163943707](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615163943707.png)<br><font color="red">公式的证明要会！对于+B或-B补数都是mod 2<sup>n+1</sup>+X，因此两者相同</font>
  
- 例题
  - ![image-20200615164840191](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615164840191.png)<br><font color="red">此处设题有漏洞，假设了机器字长为4位，符号位是1位，要强化注意对机器数的概念！</font>
  - [B]<sub>补</sub>→[-B]<sub>补</sub>的方法见上面的反码部分！（包含符号位在内每位取反，末位加1）<br>符号位溢出部分直接省略不计！<br>![image-20200615172609308](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200615172609308.png)
  
- 溢出判断

  1. 1位符号位判溢出：最高有效位的进位$\bigoplus$符号位的进位 = 1 即溢出
     - 若数值部分进位，原符号位0的会变成1，原符号位1的会变成0 → 符号位与原本的相反 → 溢出
     - 若符号位进位，原符号必定是从1变成0 (10) → 溢出
     - 若数值部分和符号位都进位，原符号位1还会是1 → 不算溢出
     - 有无溢出看得就是符号位是否相反
     - ps黄字确实有写错的部分，例2的A-B答案不是10，000……
  2. 2位符号位判溢出
     - ![image-20200616105830006](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616105830006.png)
     - 两符号位不同即溢出
  3. 硬件
     - ![image-20200616111058358](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616111058358.png)
     - ![image-20200616111142131](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616111142131.png)
     - A：ACC。G<sub>A</sub>的A是Add，S是Subtract，表示是做加法还是减法。
     - 取反就加个反相器就行了。补数之后再加上个1。A和X都是n+1位
     - 

**乘法运算**

- 运算由加和移位实现
  - ![image-20200616120056767](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616120056767.png)
  - ![image-20200616120038120](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616120038120.png)
  - ![image-20200616120012700](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616120012700.png)
  - ![image-20200616115931941](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616115931941.png)
  - 硬件
    - 需要3个寄存器，2个具有移位功能，抱持累加和的高低位以及乘商寄存器需要移位
    - 还要1个全加器
- 原码乘法：加上符号位的处理
  - 公式：[x]<sub>原</sub> · [y]<sub>原</sub> = x<sub>0</sub>$\bigoplus$ y<sub>0</sub>· (0.x<sub>1</sub>x<sub>2</sub>x<sub>3</sub>...x<sub>n</sub>) (0.y<sub>1</sub>y<sub>2</sub>y<sub>3</sub>...y<sub>n</sub>) = x<sub>0</sub>$\bigoplus$ y<sub>0</sub>· x\*y\*	//x\*是x的绝对值，y\*是y的绝对值
  - ![image-20200616144420403](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616144420403.png)<br>![image-20200616144447478](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200616144447478.png)
  - 硬件
    - Q寄存器的高位部分会逐渐被累加和的低位部分占据
    - 计数器用来记录移位次数，n位的数字需要移位n次
    - S是符号位
    - G<sub>M</sub>：乘法标志
    - 做一次加法就做一次移位，加法和移位是由乘数的最低位控制
    - 当乘数最末位的值是1时控制门打开，被乘数从X通过控制门送到加法器

**除法运算**

- 恢复余数法：为了实现减法操作，引入了y的补码，<font color="blue">逻辑左移</font>
  - ![image-20200618140426268](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618140426268.png)
  - ![image-20200618140355439](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618140355439.png)
- 不恢复余数法/加减交替法：先用-y去加溢出的话直接移位之后在拿+y补，不理解的话直接拿除法算式计算一边
  - 当上商0时，(x\*-y\*)<<1+y\* = 2(x\*-y\*)+y\*，也就同于恢复余数法中的x\*<<1-y\*
  - 上商1时
  - ![image-20200618145739607](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618145739607.png)
  - ![image-20200618150928226](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618150928226.png)

## 浮点四则运算

**加减法运算**

x = $S_{x}\cdot2^{j_{x}}$，y = $S_{y}\cdot2^{j_{y}}$

1. 对阶：
   1. 求阶差
   2. 通过右移方式使阶码j<sub>x</sub>=j<sub>y</sub> //不能左移，左移可能会造成最高位的溢出导致数据出错，右移只会影响精度
2. 尾数求和
3. 规格化：为了尽可能地提高计算机中浮点数的表示精度
   - 定义，|S|尾数的范围在1/基值~1之间
     - ![image-20200618154803748](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618154803748.png)
   - 对于规格化数通常采用以下的方法而不使用定义，但会存在两个点的特例-1/2&-1
     - ![image-20200618155035007](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618155035007.png)
     - ![image-20200618155339085](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618155339085.png)
     - 左规右规  
       - 由于补数为负数时是相反当为1.1..时其实是-0.0..，因此需要左移放大
       - 符号位两位是为了判断溢出，符号位不同就是溢出，就需要右规
       - ![image-20200618155733112](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618155733112.png)
4. 舍入
   1. 0舍1入法
   2. 恒置“1”法
5. 溢出判断

**例题**

这个例题很重要有很多运算关键点！①补码移位要如何添加 ②移位后阶码如何改变 ③补码的形式：x的补码是针对于尾数部分的，因此尾数会因负值而改变，前面阶码照抄就好，但在专门计算阶码时仍需注意阶值为负的情形与正的有所区别

- ![image-20200618172747558](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618172747558.png)
- ![image-20200618172814196](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618172814196.png)

**乘除法**：补码方便加减，原码实现乘除，所以浮点乘除不那么重要，408考纲不含这个，老师说自学！

## 算数逻辑单元（本节可能不重要？不太清楚）

**ALU电路**

ALU是组合逻辑电路，无记忆结果功能，所以需要再A<sub>i</sub>B<sub>i</sub>端连接寄存器

F表示输出，K控制所做的运算类型

![image-20200618181250492](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618181250492.png)

**快速进行链**

1. 并行加法器<br>![image-20200618182026232](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618182026232.png)
   - 输入端：AB为输入，C为从低位来进位
   - 输出端：S为对应加法的和的结果的1位，另一个C为向高位的进位
   - 如果输入的为1、00或者111，那么对应S的值就是1![image-20200618181917610](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618181917610.png)
   - 当2个或以上的输入为1时就会产生进位![image-20200618182011623](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618182011623.png)
   - 这种输入->输出的机器FA称为全加器
   - ![image-20200618183319030](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618183319030.png)<br>因此d<sub>i</sub>=A<sub>i</sub>B<sub>i</sub>称为本地进位，t<sub>i</sub>=A<sub>i</sub>+B<sub>i</sub>被称为传送条件当它为1时会将C<sub>i-1</sub>的值传送到C<sub>i</sub>
   - ![image-20200618183626497](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618183626497.png)
2. 串行进位链：传送进位的电路，在加法器中可以独立出“进位产生”的这部分电路
   - ![image-20200618184006941](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618184006941.png)（by笛摩根定律，给跪了我知道这个定律但完全想不到去使用！）
   - 通过上面的表达式就可以建构电路![image-20200618184200703](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618184200703.png)
   - 如果一个与非门的延迟时间为t，按上图所构成的4位全加器产生进位的全部时间为8t<br>n位全加器就需要2nt
3. 并行进位链（先行进位/跳跃进位）：提高进位的速度，进位时间为2.5t
   - 用“与或非门”![image-20200618204000697](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618204000697.png)
   - 组与组间串行连接，组内并行进位![image-20200618204056573](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618204056573.png)
   - 大组与大组间串行连接，组内分批同时进位![image-20200618204120543](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200618204120543.png)
     - ![image-20200619124017906](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200619124017906.png)
     - ![image-20200619124957160](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200619124957160.png)

# 第三部分：CPU-CU

# 控制器

## 机器指令

**指令格式**

操作码+地址码

1. 操作码：长度可固定也可改变
   - 扩展操作码技术：减少1种1111的操作码作为拓展标志，从而拓展出最多2<sup>4</sup>条地址数
2. 地址码
   - 通过减少地址字段的个数，使每个地址字段能占更多位，从而扩大寻址范围
   - 例如：假设指令字长为32位，其中操作码占八位
     - 四地址指令：每个地址字段各占6位，寻址范围=2<sup>6</sup>=64，四次访存<br>![image-20200620171826188](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200620171826188.png)
     - 三地址指令：有计数器PC存放当前欲执行指令地址，并自动生成下一条指令地址
     - 二地址指令：中间结果保存在ACC而非主存中，3次访存
     - 一地址指令：地址字段为24位，寻址范围可达=2<sup>24</sup>=16KB，ACC即存放参与运算的操作数又存放中间结果，2次访存
     - 零地址：空操作、停机等等，只有操作码而无地址

**指令字长**

取决于：操作码长度+操作数地址长度+操作码地址个数

字长可固定，也可按照字节的倍数进行变化

## 操作数的类型和操作种类

**操作数类型**

- 地址：for跳转指令

- 数字

- 字符

- 逻辑数：for逻辑运算

**数据在存储器中的存放方式**

1. 从任意位置开始存储：不浪费存储资源但访问速度慢
2. 从一个存储字的起始位置开始存储：访问速度快，但浪费了太多存储资源
3. 边界对齐方式：从地址的整数倍开始访问，折中

**操作种类**

1. 数据传送
2. 算数逻辑操作
3. 移位操作：算数移位、逻辑移位、循环移位
4. 转移
   1. 有条件跳转
   2. 无条件跳转
   3. 调用和返回
   4. 陷阱指令：出现异常时，由CPU自动执行的隐指令
5. 输入输出

[汇编指令大全](https://wenku.baidu.com/view/c087cea0f524ccbff12184a3.html)

## 寻址方式

1. 指令的寻址
   1. 顺序寻址：(PC)+1→PC //这边的1其实是1条指令的长度
   2. 跳跃寻址：由移转指令指出
2. 指令中数据的寻址<br>![image-20200621152617486](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200621152617486.png)
   - 形式地址并不一定是操作数的真实地址，要根据寻址特征经过一系列的寻址运算才能变有效地址
   - 寻址特征：寻址的方式
   - 寻址方式：请自行看课本！

## RISC技术

28原则

RISC：精简指令计算机，Reduced Instruction Set Computer

- 选择使用频度高的简单指令，来完成复杂指令的功能 → 加快执行速度
- 指令长度固定、指令格式种类少、寻址方式少
- 只有LOAD/STORE指令访存，其他只能在寄存器中
- CPU中有多个通用寄存器
- 采用流水线方式来在一个时钟周期内完成一条指令
- 采用逻辑组合实现控制器

CISC：复杂指令计算机，Complex...

- 指令系统庞大
- 指令长度不固定、指令格式种类多、寻址方式多
- 访存指令不受限制
- CPU中设有专用寄存器
- 大多数指令需要多个时钟周期完成
- 采用微程序控制器

**比较**

- RISC更能充分利用VLSI芯片面积
- RISC提高运行速度，且便于实现指令流水
- RISC便于设计可降低成本，提高可靠性
- RISC不易实现指令系统兼容

# CPU的结构和功能

## CPU的结构

cpu的功能：对指令进行解释，包含了控制器的功能+运算器的功能，主要可划分为5大部分——指令控制（PC、IR：Instruction register）、操作控制（CU时序电路）、时间控制（CU）、处理中断（中断系统）、数据加工（ALU）

控制器的功能：

- 取指令→指令控制
- 分析指令
- 执行指令→操作控制，各种操作命令要有先后顺序，因此还有时间控制
- 控制程序输入及结果输出
- 总线管理
- 处理异常情况和特殊请求→处理中断

运算器的功能：实现算数运算and逻辑运算→数据加工

![image-20200625091226290](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200625091226290.png)

**CPU寄存器的分类**

1. 用户可见寄存器
   1. 通用寄存器
   2. 数据寄存器
   3. 地址寄存器
   4. 条件码寄存器 //条件码：是否需要跳转等等
2. 依控制和状态寄存器进行分类
   1. 控制寄存器![image-20200625091828066](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200625091828066.png)
   2. 状态寄存器
      - 状态寄存器：用于存放条件码
      - PSW寄存器（Program State Word寄存器）：用于存放程序状态字，为了在程序中断后还能回到断点继续执行给定程序，在程序中断或转子程序时，就要保存程序的运行现场和程序的断点，把软硬件状态相关的寄存器集合成一个大的寄存器，这就是程序状态字

**控制单元CU和中断系统**

1. CU产生全部指令的微操作命令序列（在第4篇介绍）
   - 组合逻辑设计：硬连线逻辑
   - 微程序设计：存储逻辑
2. 中断系统 //后续介绍

**ALU** //第六章已介绍

## 指令周期

![image-20200629094958145](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200629094958145.png)

NOP指令没有执行阶段

间接寻址需要取操作数的地址和取操作数两次访存，因此执行周期会较长，会专门加一个间址周期

![image-20200629095814902](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200629095814902.png)

具有中断周期的指令周期

指令周期的流程

![image-20200629101551476](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200629101551476.png)

CPU的访存

1. 取指令：取址周期
2. 取地址：间址周期
3. 存取操作数或结果：执行周期
4. 保存程序断点：中断周期

CPU工作周期的标志

![image-20200629103918456](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200629103918456.png)

| NAME | INFORMATION |
| ---- | ----------- |
| FE   | 取址周期    |
| IND  | 间址周期    |
| EX   | 执行周期    |
| INT  | 中断周期    |

**指令周期数据流**

**取址**

![image-20200629110133188](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200629110133188.png)

**间址周期数据流**

![image-20200629113846394](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200629113846394.png)

间址最开始会是在MDR或者IR中给出地址

**执行周期数据流**

不同指令的执行操作差异大，会在第9章详细介绍

**中断周期数据流**

1. 保存断点：先需要由CU控制断点会保存在内存的哪个位置。CU会发出写命令。中断指令要返回的地址是多少保存在PC中，所以会由PC给到MDR再存入内存

2. 形成中断服务程序的入口地址：中断服务程序的入口地址会由CU给出直接写入到PC中（这部分会在8.4节详细介绍）

![image-20200629114829003](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200629114829003.png)

## 指令流水

**提高机器速度**

1. 提高访存速度：高速芯片、Cache、多体并行
2. 提高I/O和主机间的传送速度：中断、DMA、通道、I/O处理机、多总线
3. 提高运行器速度：高速芯片、改进算法、快速进位链
4. 提高整个处理机的处理能力：改进系统结构、开发系统并行性

**系统并行性**

并行

- 并发：同一时间段
- 同时：同时

并行性的等级

- 过程级：两个程序并行（粗粒度）
- 指令级：两条指令之间在同一时刻都处于被解释的状态（细粒度）

指令的串行执行

![image-20200630095149996](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200630095149996.png)

//但这样取指令部件忙的时候，执行指令就会处于空闲状态，总有一个部件会空闲，利用率低

指令的二级流水

![image-20200630095311259](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200630095311259.png)

//在理想情况下，流水线处于满负荷的运行状态，指令周期减半，速度提高一倍

**影响指令流水效率加倍的因素**

1. 执行时间>取址时间 //取指时间是固定的，但执行时间会因为指令的复杂程度而提高，可以再取指令部件和执行指令部件中增加一个缓冲区，用于缓冲取指，执行部件完成后就可以去缓冲区取指令执行
2. 条件转移指令对指令流水的影响 //上条指令执行结束后，才能确定下条指令的地址，造成时间损失

**指令的六级流水**

![image-20200720203259874](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200720203259874.png)

完成1条指令时间=6个时间单位

串行执行所需时间=6×9=54

六级流水=6+9-1=14 

**影响指令流水线性能的因素**

1. 结构相关：不同指令在同一时刻争用同一部件造成资源冲突
   - 解决方法：
     - 停顿
     - 将指令存储器和数据存储器分开
     - 指令预取技术
2. 数据相关：不同指令重叠操作时，可能改变操作数的读写访问顺序
   - 先写后读相关RAW
   - 先读后写相关WAR
   - 先写后写相关WAW
   - ![image-20200720204226704](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200720204226704.png)
   - 解决方法：后推法（推后读or推后写），采用旁路技术（输出端生成结果后直接送到第二条指令进行运算，无需等待）
3. 控制相关（转移指令可能会造成指令的损失）

**流水线性能**

| NAME                | INFORMATION                                                  |
| ------------------- | ------------------------------------------------------------ |
| 吞吐率              | 单位时间内流水线所完成指令或输出结果的数量<br>· 最大吞吐率<br>· 实际吞吐率 |
| 加速比S<sub>p</sub> | 流水线速度与非流水线速度之比                                 |
| 效率                | 流水线各功能段的<font color="blue">利用率</font>             |

![image-20200722205012780](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200722205012780.png)

若不能理解，请看上面的六级流水图

![image-20200722205415227](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200722205415227.png)

速度与时间成反比

![image-20200722205729763](C:\Users\AAA\AppData\Roaming\Typora\typora-user-images\image-20200722205729763.png)

从流水线时空图看就是占有的面积/时间和空间轴围城的面积

**流水线的多发技术**



# 中断系统

