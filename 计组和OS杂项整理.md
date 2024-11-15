### 计算机组成原理&OS概念汇总



#### 第一章 计算机系统概述

+ 计算机系统层次结构

  + 5个基本分级：微程序机器层（硬件，硬件执行微指令）、传统机器语言层（机器，微程序解释机器指令）、操作系统层（混合，操作系统定义和解释软件指令）、汇编语言层（汇编程序支持和执行）、高级语言层（高级语言编译程序支持和执行）
  + ISA（指令集体系结构）：定义了一台计算机可以执行的所有指令集合，每条指令规定了计算机执行的操作，以及所处理的操作数存放的地址空间和操作数类型

+ 计算机系统基本组成：**硬件系统**和**软件系统**组成了一个完整的计算机系统

  （硬件：有形的物理设备；软件：在硬件上运行的程序和相关数据及文档）

  + 计算机系统硬件基本组成：IO设备、存储器（主存和辅存【按地址存取：按存储单元地址进行存取】）、运算器和控制器

    + 存储体：数据通常存储在**存储体**当中，而存储体又由**存储单元**（存放一串二进制代码）构成

      存储字：存储单元内二进制代码的组合

      存储字长：存储单元中二进制代码的长度

      + **MAR**用于寻址（位数反映最多可寻址存储单元个数，**与PC位数相同**）
      + **MDR位数**一般**等于存储字长**

    + ALU必须具备ACC（累加器）、MQ（乘商寄存器）、X（操作数寄存器），并且有**PSW（标志寄存器）**

    + **控制器=PC+IR+CU；CPU=ALU+控制器**

    + PC与MAR间有一条直接通路

  + 计算机软件

    + 三类翻译程序
      + 汇编程序（汇编器）：将**汇编语言**翻译成**机器语言**
      + 解释程序（解释器）：将源程序中语句**按执行顺序**逐条翻译成**机器指令并立即执行**
      + 编译程序（编译器）：将高级语言翻译成**汇编语言或机器语言程序**

  + 计算机软件和硬件关系：对某一功能，若其能用硬件实现，又可用软件实现，则其在**软硬件上是逻辑等价的**

+ 计算机系统工作原理：

  + “存储程序”方式（研究EDVAC机时提出）
    + 冯诺依曼结构：首次提出“**存储程序**”；以**运算器**为核心
      + 特点：
        + 计算机由五个部分组成
        + 指令和数据同等地位存于存储器中，按地址寻访
        + 指令由操作码和地址码构成
        + 存储程序
        + 运算器为中心
    + 现代计算机结构：**CPU=运算器+控制器**；以**存储器**为核心
  + 高级语言程序和机器语言程序的转换
  + 程序和指令执行过程
    + “存储程序”方式：取指、译码、执行（基本）$\to$ 取指、译码/取操作数、执行、访存、写回（五段式）
    + 源程序转化可执行文件：预处理（插入库）->编译（转汇编）->汇编（转二进制）->链接（重定位文件和库函数）
    + 指令执行过程：
      + 取指令：PC->MAR->M->MDR->IR
      + 分析指令：OP(IR)->CU
      + 执行指令：Ad(IR)->MAR->M->MDR->ACC



+ 计算机性能指标：

  吞吐量；响应时间；CPU时钟周期；主频；CPI；CPU执行时间；

  MIPS；MFLOPS；

  + **机器字长（字长）**：“某16位或32位机器”，计算机进行一次整数运算（定点整数运算）所能处理的二进制数据位数
    + **字长**一般等于**通用寄存器位数**或**ALU的宽度**
    + 字长越长，数的表示范围越大，计算精度越高（通常为8的整数倍）
  + 数据通路带宽：数据总线一次所能并行传送信息的位数（外部数据总线宽度，CPU内部可能不同）
  + 主存容量：主存储器所能存储信息的最大容量（Byte），可表示为字数$\times$字长
    + MAR位数反映了**存储单元个数**
  + 吞吐量：系统单位时间内处理请求的数量（主要取决于主存储器的存储周期）
  + 响应时间：用户发送请求后，该系统做出响应并得到结果的等待时间（CPU时间【运行程序时间】与等待时间【磁盘访问、存储器访问、IO、操作系统开销】）
  + CPU时钟周期：机器内部主时钟脉冲信号宽度，**CPU工作最小时间单位**
    + CPU时钟周期=1/主频（通常主频以Hz为单位）
  + **CPI**：执行**一条指令**所需的**时钟周期数**（为平均值）
    + **IPS：每秒执行指令数；IPS=主频/平均CPI**
    + CPU执行时间：运行一个程序花费的时间（**CPU执行时间=CPU时钟周期数/主频=(指令条数$\times$CPI)/主频**）
  + FLOPS：每秒执行的浮点运算次数
  + 对…“透明“：…不需要关心具体运行方式的结构（不可见）



#### 第一章 计算机系统概述

+ 操作系统
  + 基本概念
    + 操作系统是系统资源的管理者
    + 向上层提供方便易用的服务
    + 最接近硬件的一层软件，最基本的系统软件
  + 功能：
    + 处理机管理：以进程（或线程）为基本单位
    + 存储器管理
    + 文件管理
    + 设备管理
  + 特性：
    + 并发：同一时刻能完成两种或两种以上的工作（微观上交替执行）
    + （资源）共享：**多个并发**执行进程共同使用资源（并发为前提）
      + 互斥共享：一段时间内只允许一个进程访问该资源【临界资源：栈、表格和变量】
      + 同时访问：一段时间可多个进程“同时访问”
    + 虚拟：将一个物理上的实体变为若干逻辑的对应物
      + 时分复用：虚拟处理器
      + 空分复用：虚拟存储器
    + 异步：执行并非一贯到底，走走停停，以不可预知的速度向前推进（运行环境相同，**OS保证**多次运行进程后得到相同结果）
  + 命令接口：联机控制方式（交互式）和脱机命令接口（批处理）
  + 程序接口：由一组系统调用（应用程序请求OS服务的**唯一方式**）组成



+ 操作系统的发展历程
  + 手工操作（无OS）
  + 批处理阶段：解决CPU与IO速度不匹配问题（单道和多道）【按时钟管理衡量作业完成程度】
    + `windows98`：单用户多道作业
  + 分时操作系统：作业流转快，具备及时性
  + 实时操作系统：硬~（绝对不违反）、 软~（偶尔违反）【按截止时间控制运行】
  + 网络操作系统（网络内资源共享，不同任务）和分布式系统（每台计算机同等地位，并行运行，同一任务）



+ 两种指令：
  + 特权指令：如I/O指令、关中断、内存清零、存取用于内存保护的寄存器、送PSW到程序状态字寄存器等指令
  + 非特权指令：不能直接访问系统的软硬件资源，仅限访问用户地址空间
+ 两种CPU运行模式：目态（用户态）、管态（内核态）【访管指令转换，非特权指令】
  + 内核->用户：一条更改PSW的特权指令
  + 用户->内核：由中断引起，硬件自动完成
+ 中断和异常的处理：**硬件实现了用户态转内核态**（释放进程占有的资源就通过中断实现）
  + 中断
    + 异常（内中断）：与当前执行指令有关，信号来源CPU内
      + 故障：执行出错（可能可由CPU修复）【软件】
        + 修复完成，重新执行此条引发异常的指令
      + 自陷：系统调用【软件、非特权】
      + 终止(Abort)：致命错误【硬件中断】
    + 外中断：与当前指令无关，信号来自CPU外部【每个指令周期末尾，CPU检查】
      + 可屏蔽中断 INTR【时钟中断】
      + 不可屏蔽终端 NMI【I/O中断请求】
    + **与子程序调用区别**：
      + 中断处理程序与被中断程序相互独立
      + 中断产生通常随机，子程序是`call`产生
      + 调用子程序是完全软件过程
      + 中断处理程序入口地址可由**硬件向量法**产生向量地址，子程序入口地址由`call`给出
      + 保护PC值：前者由**中断隐指令**完成，后者由压程序栈完成
      + 多个中断请求同时发出时，需要**进行裁决**
+ 系统调用：操作系统库提供的子功能，每条都有**唯一的系统调用号**
  + 处理过程（P19）
  + 转核心态实例：
    + 用户进程系统调用
    + 发生中断（`trap`）
    + 用户程序产生一个错误状态
    + 用户程序企图执行特权指令
+ 程序的链接和装入
  + 编译：由编译程序将用户源代码编译为若干模块
  + 链接：由链接程序编译后形成一组目标模块，与所需库函数链接，形成完整装入模块
    + 静态：与库函数连接之后不再拆开
    + 装入时动态链接：装入内存时，边装入边链接
    + 运行时动态链接：程序执行时，需要某目标模块才链接，**未使用的都不会调入内存和链接到装入模块上**
  + 装入：把装入模块入内存运行
    + 绝对装入：编译时将逻辑地址转换为物理地址（若知道程序将放到内存的那个位置，产生绝对地址的目标代码）【单道程序阶段（无操作系统）】
    + 可重定位装入（早期多道批处理）：编译、链接后的装入模块的始址通常从0开始，指令和数据地址相对于始址。
      + 根据内存的当前情况，将装入模块装入内存的适当位置。装入内存时，再进行地址转换（相对地址修改过程称为重定位：一次性【静态重定位】）
    + 动态运行时装入（现代操作系统）：地址转换推迟到程序真正要执行时才进行【装入内存后地址均为相对地址（重定位寄存器）】
+ 进程内存映像（P179）！！



+ 操作系统结构
  + 分层：每层只能调用紧邻它的低层功能和服务（单向依赖）
  + 模块化：分为若干模块，模块间能通过接口进行通信
  + 宏内核：主要功能模块作为整体运行在核心态，各管理模块共享信息
  + 微内核：最基本功能保留在内核，划分为微内核和多个服务器，
  + 外核：内核负责进程调度，外核负责为用户进程分配（保证资源使用安全）



+ 操作系统引导过程（P30）



+ 虚拟机：覆盖了软件的机器称为扩充机器（虚拟机）
  + 第一类虚拟机管理程序（运行于硬件上）
    + 它是唯一一个运行在最高特权级的程序
    + 裸机上运行并且具备多道程序功能（真实划分硬件）
    + 虚拟机作为用户态的进程使用，不允许执行敏感指令
  + 第二类虚拟机管理程序（VM）
    + 执行系统指令会被截获转化为VMM的系统调用（对宿主机）



---



#### 第二章 数据的表示和运算

+ 数制与编码

  + 二进制使用原因：
    + 两个稳定状态物理器件便可以表示二进制的每一位
    + 二进制与逻辑真假相对应，便利
    + 二进制编码和运算规则，逻辑门电路能方便表示

+ 定点数的编码表示

  + 机器数：正负符号数字化的数

  + 原码表示（$-(2^n-1)\leq x\leq 2^n-1$，n+1位）
    $$
    \begin{align}
    [x]_原=
    \begin{cases}
    0,x,&0\leq x<2^n\\
    2^n-x=2^n+|x|,&-2^n<x\leq0
    \end{cases}
    \end{align}
    $$
    **两种0的表示**：0000 0000 和 1000 0000

  + 补码表示（$-2^n\leq x\leq 2^n-1$）：由于0唯一，并且表示了$-2^n$，范围增加

  + C语言：强制类型转换时位值不变，长变短截断，短变长符号扩展

    + 8位：char【ASCII： A=65，a=97】
    + 16位：short
    + 32位：int、long（32位机的） float
    + 64位：long（64位机的）double
    + 128位：long double



+ 运算方法和运算电路
+ 基本运算部件：
  + 加法器（带标志）
    + CF标志位：$CF=C_{out}\oplus C_{in}$（**最高位进位和借位异或**）
    + OF标志位：$OF=C_{n}\oplus C_{n-1}$（符号位和数字最高位进位异或）
    + SF标志位：符号位为1（一般为负时）
    + ZF标志位：判断为0
  + 运算器 = 算术逻辑单元（ALU）+ 移位器 + 状态寄存器（PSW）+ 通用寄存器 + …
+ 乘除运算（P45）：讲不清
  + 乘法电路基本结构
    + 使用64位乘积寄存器（乘数和结果暂存）储存32位的数相乘
    + 对64位寄存器进行32次的逻辑右移同被乘数运算，进位放入C
  + 除法电路基本结构



+ 浮点数的表示和运算
+ 浮点数的表示
  + IEEE754标准：阶码用移码，尾数用原码
    + 1+8+23：移码+127
    + 1+11+52：移码+1023
  + 浮点数的加减运算



+ 数据的大小端方式
  + 大端：高字节放大地址，小端反之
+ 边界对齐：
  + 条件
    + 每个成员按其类型的大小对齐（字节为单位）
    + `struct`的长度**必须是成员中最大对齐值的整数倍**（不够补空字节）
  + 对齐方式：
    + 结构体内成员按**定义先后**顺序存放
    + 长度必须是成员中**最大对齐值的整数倍**



#### 第二章 进程与线程

+ 原语：执行期间不许中断，不可分割的基本单位
  + 定义原语的**直接方法就是关中断**

+ 进程与线程

  + 进程：程序一次执行的过程（动态）；存放在磁盘中的可执行文件一系列的指令集合（静态）
    + 进程是系统进行资源分配和调度的一个**独立单位**，进程空间一般是独立的（互不访问，通过特殊系统调用实现访问）
      + 同一进程的线程天然共享进程空间
    + 进程控制块（PCB）：描述进程的基本情况和运行状态，进而控制和管理进程
    + 程序段、相关数据段和PCB构成了**进程实体**（进程映像）
    + 动态性（多个过程）、并发性（能在一段时间内同时运行）、独立性（独立运行、获得资源的独立单位）、**异步性**
  + 状态及转换
    + 创建进程->创建PCB；撤销进程->撤销PCB【PCB为进程存在的**唯一**标志，进程**页表始址**也保存于此】
      + PCB是有限的，可能分配失败
      + 撤销进程时，其子孙进程全部撤销
      + 进程终结可能有正常终止、异常结束（越界、非法指令）和外界干预
      + **进程终止的操作**：
        + 检索其PCB，读出其状态
        + 若其正在运行，则终止其并将CPU资源分出
        + 有子孙进程，则终止其子孙进程
        + 归还其持有资源给父进程或OS
        + 将该PCB所在队列删除
    + 执行前，调入资源依靠PCB保存存储始址；执行后，根据其他进程PCB恢复对应现场
    + 执行中，通过PCB同步、通信其合作进程；暂停时，通过PCB保存断点环境
  + PCB（进程控制块）：与进程一一对应
    + 主要内容（P40）
      + 进程描述信息：进程标识符（**PID**，唯一），用户标识符（UID，进程归属用户）
      + 控制管理信息：进程状态、抢占CPU的优先级
      + 资源分配清单：有关内存地址空间或虚拟空间状态、输入输出设备信息
      + 处理机相关信息（CPU上下文）：各寄存器值
    + 组织方式：链接（阻塞或就绪，链成队列）和索引（阻塞或就绪，用索引表存）
  + 程序段和数据段：程序可**被多个进程共享**，一个进程数据段可以是进程对应的程序加工处理的原始数据
  + 几种状态：运行、就绪、阻塞、创建和终止
    + 运行->阻塞（主动：资源缺失）【就绪（阻塞）挂起：就绪（阻塞）->阻塞】
    + 阻塞->就绪（被动：资源调入）

  

+ 线程实现

  + 线程：轻量级的进程，为提高多道程序并发度而构思出来的（同样有状态和转换）
    + 基本的CPU执行单元，程序流的**最小单元**；
    + 进程中的一个实体，被系统独立调度和分派的基本单位（**自己不拥有系统资源**）
    + 可共享同进程的其他线程的系统资源
    + 同一进程的CPU线程切换不会切换进程，切换时**只需保留少量寄存器内容**
    + 同进程的线程可分配给多个CPU运行
    + 一个进程可创建和撤销另一进程，而且可读、写甚至清除另一线程堆栈
  + 线程控制块：每个线程都有唯一标识符和线程控制块（记录执行寄存器和栈的执行状态【执行状态、优先级】）
  + 内核支持的线程（KLT）：
    + 操作都是在内核支持下完成
  + 线程库支持的线程（ULT）：
    + 通过进程分支语句创建线程
    + 调度以进程为单位，切换无需内核空间
    + 实现与操作系统无关

+ 进程与线程的组织与控制

+ 进程间通信：

  + 共享内存：
    + 基于数据结构（低级）
    + 基于存储区（高级）：映射到相同虚拟地址空间（页表实现），每次读取一页，退出或关闭时写回磁盘文件
  + 消息传递：以格式化的消息为单位，最广泛的进程间通信机制
    + 发送消息指明PID
    + 通过“信箱”直接通信
  + 管道：特殊的共享文件，先进先出【子进程继承父进程的管道】
    + 互斥：当一个进程对管道读写时，其它进程必须等待
    + 同步：写入一定量的数据后，写进程阻塞，直到读进程取走数据才将其唤醒【一次性，一旦被读，数据就会从管道删除】
    + 确定对方的存在



+ CPU调度与上下文切换

  + **调度（决策行为）**

    + 目的：选择进程上CPU，实现进程并发执行

    + 分类：

      + 高级调度（作业调度：作业调入时创建PCB，调出时销毁）
      + 中级调度（内存调度：将暂时不能运行的进程调到外存）
      + 低级调度（进程调度：就绪队列选取进程）

    + 实现：

      + 调度器和调度程序：由CPU运行进程和进程运行时间决定
      + 调度的时机：
        + 创建新进程
        + 进程退出
        + 运行进程阻塞
        + I/O中断发生

      + 调度方式（抢占式/非抢占式）

        + 非抢占式，运行进程终止或阻塞

        + 抢占式，运行进程k个时钟中断到时间

      + 不能调度情况：

        + 处理中断过程中，处理过程复杂
        + 进程位于OS内核程序临界区
        + 在原子过程中，原子操作不可中断

      + 闲逛进程：系统中没有就绪进程，就会调度此进程（PID=0，零地址指令）

      + 内核级线程调度和用户级线程调度：

        内核选择一个特定线程运行，通常不用考虑该线程属于哪个进程；内核不知道线程的存在，由进程内的调度程序决定线程运行，超过时间片就挂起；【用户级线程切换在同一进程中，而内核线程切换要**完整上下文切换**】

    + 典型调度算法

      + 先来先服务（FCFS）
      + 短作业优先（SJF）
      + 时间片轮转（RR）
      + 优先级调度（静态优先级和动态优先级）【系统进程>用户进程；交互型>非交互型；I/O型>计算型】
        + 非抢占式优先级：等当前进程结束
        + 抢占式优先级：立即暂停正在运行进程
      + 高响应比优先（HRRN）：$响应比R_p=\frac{等待时间+运行时间}{运行时间}>1$（克服“饥饿”现象）
      + 多级队列调度算法
      + 多级反馈队列调度算法（抢占式）

  + 上下文及其**切换（实际执行行为）**机制

    + 上下文切换：切换CPU到另一进程需要保存当前进程状态并恢复另一进程的状态
      + **内核**将旧进程状态保存在**PCB**中，然后加载经调度而要执行的新进程的上下文
      + 挂起进程存至PCB->PCB移入相应队列->选择另一进程更新PCB->恢复新进程CPU上下文->跳转新进程PCB的PC指向位置
    + 上下文切换时，需要执行大量的load和store指令，以保存寄存器的内容，因此花费较多时间
    + **与模式切换**（用户态和内核态之间的切换）**的区别**：
      + 模式切换时，CPU逻辑上可能还在执行同一进程
      + 上下文切换**只能发生在内核态**，多任务操作系统中的必需特性
    + 引起进程切换的事件
      + 当前进程时间片到
      + 有更高优先级的进程到达
      + 当前进程主动阻塞
      + 当前进程终止



+ 调度指标：
  + CPU利用率=$\frac{CPU有效工作时间}{CPU有效工作时间+CPU空闲等待时间}$
  + 周转时间=作业完成时间 - 作业提交时间
    + 平均周转时间=$\sum_{i=1}^{n}作业i的周转时间/n$
    + 带权周转时间=$\frac{作业周转时间}{作业实际运行时间}\geq 1$（越小越好）
  + 响应时间：用户提交请求到系统首次产生响应所用的时间



+ 同步（直接制约）与互斥（间接制约） P96

  + 为禁止两个进程同时进入临界区，同步机制应遵循原则

    空闲让进、忙则等待、有限等待、让权等待（并非必须，进程不能进入临界区时，应当立即释放处理器）
    
  + **实现临界区互斥方法** 
  
    + 软件方法
  
      + 单标志法：用公有变量`turn=1`表示允许进入临界区（每次进一个进程），**违背空闲让进**
      + 双标志先检查法：`flag[i]=true`表示`Pi`（i=0或1）想进入，对方想进入时就等待（先检查对方标志）；否则将自己的`flag[i]`置为`true`后进入运行，出来时再将其置为`false`【锁自己的门，之后再运行】，**违背忙则等待**
      + 双标志后检查法：先将自己标志置为`true`，再检查对方的标志`flag[i]`【可能“饥饿”】，**违背有限等待**
  
      + Peterson算法：增加了`trun`标志表示可否进入，进入前先置自己标志，检查`trun`和对方的标志，**违背让权等待**
  
    + 硬件方法
  
      + 中断屏蔽方法：关中断（**CPU只在发生中断时引起进程切换**）【不适于多处理系统，不能防止其它CPU】
      + `TestAndSet`方法：借助原子操作（TS硬件指令）【不能实现让权等待】
      + Swap方法：交换两个字（字节）内容【不能实现让权等待】
  
    + 还有互斥锁和信号量的部分不再过多赘述（大题）
  
    + 前驱后继的代码示例：
  
    ```c
    //S1->S2,S1->S3,S2->S4,S3->S4,S4->S5
    semaphore a12=a13=a24=a34=a45=0;
    
    S1(){
        V(a12);
        V(a13);
    }
    
    S2(){
        P(a12);
        V(a24);
    }
    
    S3(){
        P(a13);
        V(a34);
    }
    
    S4(){
        P(a24);
        P(a34);
        V(a45);
    }
    
    S5(){
        P(a45);
    }
    ```



+ 死锁：多个进程因竞争资源而造成一种僵局，各进程均被阻塞
  + 与饥饿差别：
    + 发生饥饿的进程可以只有一个；死锁是因循环等待对方手里的资源导致的
    + 发生饥饿进程可能处于就绪态，也可能阻塞态
  + 死锁产生原因
    + 系统资源竞争：拥有的不可剥夺资源数量不足以满足多个进程运行需要
    + 进程推进顺序非法：请求和释放资源的顺序不当，也同样会导致死锁
  + 死锁产生的**必要条件**：互斥条件、不可剥夺条件、请求保持条件和循环等待条件
  + 死锁预防：
    + 破坏互斥：互斥资源转共享（`SPOOLing` 技术）
    + 破坏不可剥夺条件
    + 破坏请求保持条件：预先静态分配和动态释放再分配
  + 死锁避免
    + 系统安全状态：系统无法找到安全序列，则称系统处于不**安全状态**（按某种顺序可使进程都顺利完成）
      + 进入不安全状态未必死锁，但死锁一定发生在不安全状态
    + 银行家算法（P153）
  + 死锁检测：资源分配图
  + 死锁解除：资源剥夺法（挂起剥夺）、撤销进程法（按进程优先级和代价撤销）和进程回退法（回退一个或多个进程至死锁前）





---



#### 第三章 存储系统

+ 存储器分类
  + 层次分类：
    + 主存储器（CPU直接访问）
    + 辅助存储器
    + 高速缓冲存储器（Cache）
  + 存储介质：磁表面存储器、磁芯存储器、半导体存储器和光存储器
  + 存取方式分类：
    + **随机存储器（RAM）**：每个存储单元可以随机存取
      + 静态：不需刷新，Cache
      + 动态：需要刷新，大容量主存系统
    + 只读存储器（ROM）：只能随即读出而不能写入（**BIOS芯片，与RAM统一编址为主存；固态硬盘**）
    + 串行访问存储器：对存储单元进行读/写操作时，需按其**物理位置的先后顺序**寻址
      + 顺序存储器：内容只能按某种顺序存取（磁带）
      + 直接存取存储器：存取信息时通常先寻找整个存储器的某个小区域，再在小区域内顺序查找（光盘）
  + 信息可保存性分类：
    + 易失性存储器：断电存储信息即消失（RAM）
      + 破坏性读出：读出后信息被破坏（相反：非破坏性读出）
    + 非易失性存储器：断电后仍然保存（ROM）



+ 层次化存储器基本结构
  + **存储容量**=存储字长*字长（如$1M\times8bit$）
  + 单位成本=总成本/总容量
  + 存储速度：数据传输速率（每秒传送信息位数）=数据的宽度/存取周期
    + 存取时间（$T_a$）：启动一次存储器操作到完成该操作所经历的时间，分为读出时间和写入时间
    + 存取周期（$T_m$）：进行一次完整的读/写操作所需的全部时间（**连续两次独立访问**存储器操作之间所需最小时间间隔）
    + 主存带宽（$B_m$）：数据传输速率，每秒从主存进出信息的最大数量
  + 层次结构：上一层存储器作为低一层存储器的高速缓存（CPU->寄存器->Cache->主存->磁盘、光盘）
    + 主存和Cache间的数据调动是由硬件自动完成的，对所有程序员是透明的



+ 半导体随机存储器（RAM）
  + SRAM-静态随机存储器（非破坏性读出）
    + 存储元用双稳态触发器（MOS），一般使用**高速缓冲器**
  + DRAM-动态随机存储器
    + 使用晶体管，**用于主存**
  + 刷新：**读后再生**，对**同一行**进行相邻两次刷新的时间间隔称为刷新周期，**通常取2ms**（刷新时不需要选片）
    + 集中刷新：在一个刷新周期内，利用一段固定时间对**所有行**刷新
    + 分散刷新：存取周期，前半部分用于正常读/写操作，后半用于刷新
    + 异步刷新：在每个刷新周期，每一行仅刷新一次，分散”死时间“；**刷新间隔=刷新周期/行数**
  + Flash存储器（U盘）【P88】



+ 主存储器
  + 存储器芯片由**存储体、I/O读写电路、地址译码电路和控制电路等部分**组成
    + 【地址线+数据线+片选线+读写线 (除电源和接地端)】
+ **多模块存储**
  + 单体多字：每个存储单元存储m个字，总线宽度为m个字（一次读一字），从**同一地址**（连续存储）取m条指令，逐条送CPU执行【一条指令耗费1/m个存取周期存取】
  + 多体并行存储器
    + 高位交叉编址
      + 分为多个模块，每个模块有n个单元，访问连续存储块时总先在一个模块中访问，直至该模块访问完（因为多个低位地址在同一模块）【不能各个模块并行，因为指令顺序存储】

    + **低位交叉编址**：低位按**取模**放在不同模块中，模块号=单元地址%m
      + **轮流启动方式**：$m\geq T/r$（模块数不小于存取周期/总线周期）【流水线方式：连续取m个字$t_1=T+(m-1)r$】
      + 同时启动方式：所有模块的数据位数相加为一次读写的字大小（如：m=4，每个模块16位 -> 每次读/写64位）

+ DRAM芯片和内存条
  + **MDR的位数**与**数据线**位数相同，**MAR的位数**与**地址线**位数相同
  + **构成**：假定一个$2^n\times b$位的DRAM芯片存储序列，行数为r（行地址位数为$\log_2r$），列数为c（$\log_2c$），则$2^n=r\times c$（行数要尽量少，减少刷新次数）
  + 访存过程（P89）
  + 地址引脚复用技术：**行地址和列地址**分两次输入，减少一半地址引脚数



+ 主存储器和CPU之间的连接
  + 主存储器通过数据总线、地址总线和控制总线与CPU相连
  + **数据总线位数*工作频率 正比 数据传输速率**
  + **地址总线位数**决定了可寻址的**最大内存空间**
  + 控制总线指出总线周期类型（读/写）和本次输入输出操作完成时刻



+ 主存容量扩展【a为地址总线位数、d为数据总线位数：$M_{max}=2^a\times d$】
  + 位扩展：数据字长（单字位数）扩展（对数据总线）
  + 字扩展：地址位数扩展
  + **字位扩展**：两个同时扩展 -> 总线数=片选线+地址线+数据线
    + 线选法：一根线控制此芯片是否激活
    + 片选法：用译码器变为$2^n$个信号控制




+ 外部存储器
  + 磁盘存储器（读写串行）
    + 组成：
      + 驱动器：转动并进行读写的
      + 控制器：驱动器和主机接口，有IDE、SCSI、SATA、ATA标准等

    + 存储区：磁头数（记录面数量）、柱面数（弧形切分）、扇区数（扇形切分）
    + 高速缓存：**内存**开辟区域，缓冲，**按“簇”写磁盘**
    + 指标：
      + 非格式化容量 = 记录面数 * 柱面数 * 每条磁道磁化单元数
      + 数据传输速率 = 转数 * 磁道字节密度
      + 磁盘地址：柱面号 盘面（磁头号） 扇区号

  + 固态硬盘（SSD）（基于闪存EEPROM、ROM）
    + 随机写慢（以页（块）为单位擦除，支持随机访问）




+ 高速缓冲存储器（Cache）
  + 基本原理：Cache和主存间映射方式
  + Cache中主存块替换算法；Cache写策略
  + 磨损均衡
    + 动态：自动选较新的写
    + 静态：老的不用写，新的优先读写



+ 虚拟存储器（这里在大题总结里）
  + 虚拟存储器的基本概念：
  + 页式虚拟存储器【每个进程都有一个页表基址寄存器，存放该进程的首地址（页表存放主存地址）】
    + 基本原理
    + 页表
    + 地址转换
    + TLB
  + 段式虚拟存储器的基本原理
  + 段页式虚拟存储器的基本原理





#### 第三章 内存管理

+ 内存管理功能：内存空间分配与回收、地址转换、内存空间的扩充（虚拟存储技术）、内存空间扩充、存储保护（各进程在各自存储空间）
+ 内存管理概念：
  + 逻辑地址：32位系统逻辑地址空间范围为$0\to2^{32}-1$（虚拟地址其**不一定**对应虚拟存储器空间的一一位置，可能包含段地址形式）
  + 物理地址空间：物理内存单元集合
  + 地址变换：通过MMU转换逻辑地址为物理地址
  + 内存共享：只读区域才可共享
  + 内存保护（两种方法）：
    + 在CPU中设置一对上下限寄存器
    + 采用重定位寄存器（基址寄存器）和界地址寄存器（限长寄存器）
  + 内存分配与回收
    + 内部碎片：分配给某进程的内存区域中，没有被使用的部分
    + 外部碎片：内存中某些分区太小，无法被使用
+ 连续分配管理方式（单一连续分配、固定分区分配(均等、不均)、**动态分区分配**(空闲分区链【可合并式】)【紧凑技术克服外部碎片(动态重定位寄存器)】）
  + **动态分区搜索算法**
    + 基于顺序搜索
      + 首次适应：每次从开始搜索【地址递增】
      + 邻近适应：每次从上次搜索结束处开始【地址递增】
      + 最佳适应：从最小容量分区开始【容量递增】
      + 最坏适应：从最大容量分区开始【容量递减】

    + 基于索引搜索
      + 快速适应：根据进程长度找到最小可容分区链表 拿出第一块分配
      + 伙伴系统：规定分区大小均为$2^k$，当需要n的分区，在大小为$2^{i-1}<n\leq2^{i}$ 空闲分区链查找；否则，表示$2^i$空闲分区耗尽，等分$2^{i+1}$分区一个，一半用于分配，另一个用于放入$2^i$分区链
      + 哈希算法：构建一张以空闲分区为关键字的哈希表

  + **页式管理**
    + 页号：**进程**的**逻辑地址空间**的编号
    + 页框号：**内存空间**的每个页面的编号【内存空间分为固定大小分区（页框、物理块）】
      + 虚拟页大小=页框大小=页内偏移量上限
      + 页号=地址/页大小；页内偏移量=地址%页大小

    + 一级页表的虚地址：页号（对应页框号转换）+页内偏移量

  + 段式管理：用户进程**逻辑地址空间**划分为**大小不等**的段【很可能越界】
    + 段表：段号+段内偏移量

  + 段页式管理：每个进程可能只有一个段表，但有很多页表




+ 虚拟内存管理
  + 传统存储管理：一次性（作业一次性装入内存才能运行）、驻留性（作业装入内存后一直驻留内存）
  + 虚拟存储器：多次性、对换性（作业无法常驻内存）、虚拟性（扩充了内存容量）
  + 必须条件：
    + 一定容量的内存和外存
    + **页表机制**（或段表机制）作为主要数据结构
      + 请求页表项：页号、物理块号、状态位（是否在内存）、访问字段（一段时间被访问次数）、修改位（在内存是否被修改过）、外存地址（外存存放地址）
    + **中断机构**，资源未调入会中断【内中断（异常）】
    + **地址变换**机构，逻辑地址和物理地址相互转换
+ 虚拟内存基本概念
  + 请求页式管理（P214）
  + 页框分配
    + 驻留集：给特定进程分配的页框大小
    + 内存分配策略：
      + 固定分配局部策略：每个进程固定分配空间（不变）
      + 可变分配全局置换：每个进程在运行时可借用未分配的资源
      + 可变分配局部置换：只允许每个进程使用自己分配到的空间，再适当增减**直至缺页率到达合适**程度
    + 物理块调入算法
      + 平均分配：可供分配物理块平均分配各进程
      + 按比例分配：按进程大小比例
      + 优先权分配：通常按一部分比例分配，一部分按优先权分配
  + 页置换算法：【缺页中断未必置换】
    + 最佳置换算法（OPT）：将以后不用的直接调出（或最长时间不被使用的）【往后看】
    + FIFO
    + 最近最久未被使用（LRU）【逆向来看】
    + **CLOCK**时钟置换（P219）：使用循环链表轮转
      + 简单时钟：入表标记为1，满且无0时轮转一圈后至队首全体减1
      + 改进时钟：增加了一位修改位M，次佳为最近未被访问且已被修改
+ 内存映射文件（Memory-Mapped Files）：操作系统向应用程序提供的一个系统调用（磁盘文件和进程虚拟地址空间映射）
  
  + 虚拟存储器性能的影响因素
    + 缺页率：主要因素
    + 写回磁盘的频率
  + 改进方式：
    + 适当增加分配的物理块数
    + 选择好的页面置换算法，如LRU和CLOCK
    + 使用写回法



+ 可能不会考的（抖动和工作集）
  + 抖动：刚换出的页面马上又要换入内存，刚刚换出的页面马上又要换出内存
    + 分配给每个进程的物理块太少，不能满足进程正常运行的基本要求，致使每个进程在运行时频繁出现缺页，必须请求系统将所缺页面调入内存
  + 工作集：某段时间间隔内，进程要访问的页面集合（外存）
    + 工作集W可由时间t和工作集窗口尺寸$\Delta$来确定
    + 驻留集大小不能小于工作集（调入内存资源>进程运行所需资源）



---



#### 第四章 指令系统

（大题整理那儿）

+ 指令格式的基本概念
  + 机器指令：指示计算机执行某种操作的命令（**最小功能单位**）
  + 机器字长：CPU进行一次整数运算所能处理的二进制数据位数
  + 指令字长：一条指令所包含的二进制代码，其取决于操作码的长度、地址码长度和地址码个数【通常为字节整数倍】



+ 指令格式



+ 寻址方式



+ CISC和RISC的基本概念



+ 高级语言和机器级代码之间的对应
+ 选择结构、循环结构的机器级表示
+ 过程（函数调用的机器级表示）



---



#### 第五章 中央处理器

+ CPU
  + 功能
    + 指令控制：取指、分析和执行指令
    + 操作控制：将操作信号送到相应部件
    + 时间控制
    + 数据加工：运算
    + 中断处理：针对出现异常和中断请求
  + 结构：运算器和控制器
    + **用户可见寄存器**：通用寄存器组（基址/变址）、程序状态字（PSW）、程序计数器（PC）、累加寄存器（ACC）、移位寄存器（SR）
    + **用户不可见寄存器**：**MAR、MDR、指令寄存器（IR）**、暂存寄存器



+ 指令执行顺序：取指、译码/取数、执行、访存、写入
+ 指令执行方案：
  + 单周期处理器：所有指令都选用相同执行时间来完成
  + 多周期处理器：对不同类型指令选用不同执行步骤
  + 流水线处理器：各指令处在不同执行步骤，每个阶段所用资源大概率不同（可并行执行）



+ 数据通路
  + 组成：
    + 组合逻辑元件（操作元件）：任何时刻输出仅取决于当前输入，**不含存储信号的记忆单元**
    + 时序逻辑元件（时序逻辑元件）：任何时刻输出取决于当前输入**还有以前的**，包含存储信号的记忆单元
  + 分类：
    + CPU内部单总线
    + CPU内部多总线
    + 专用数据通路
  + 功能：
    + 通用寄存器之间传送数据
    + 从主存读取数据
    + 将数据写入主存
    + 执行算术或逻辑运算
    + 修改程序计数器值



+ 控制器
  + 功能：
    + 从主存取指令，指出下条指令在主存位置
    + 对指令译码或测试，产生对应的控制信号
    + 指挥并控制CPU、主存、I/O之间数据流动方向
  + 工作原理



+ 异常和中断机制
  + 异常和中断的基本概念
  + 异常和中断的分类
  + 异常和中断的检测和响应



+ 指令流水线（流水线相关见大题整理）
  + 指令流水线的基本概念
  + 指令流水线的基本实现
  + 冒险处理
  + 超标量和动态流水线的基本概念



+ 多处理器基本概念
  + 分类
    + 单指令流单数据流（SISD）：包含一个处理器和一个存储器（串行），有的使用流水线，设置多功能部件（多模块交叉）
    + SIMD：数据级并行（多个独立存储，一个主存储），一个指令控制部件多个处理单元，每个单元有自己的地址寄存器
      + 不存在MISD
    + MIMD：有独立私有存储器和独立主存，消息传递来共享数据
      + 多处理器系统（共享存储多处理器系统SMP）：共享单一地址空间
    + 向量处理器：SIMD变体，实现了直接操作一维数组向量指令集的CPU，可处理多数据集
  + 硬件多线程概念：
    + 细粒度多线程：多线程间指令不相关，**可乱序**并行执行
    + 粗粒度多线程：连续几个时钟周期都执行同一线程的指令序列，仅在当前线程出现较大开销阻塞才切换线程（Cache缺失）
    + 同时多线程（SMT）：实现指令级并行时，同时实现线程级并行
  + 多核（`multi-core`）处理器：多个处理单元（核）集成到单个CPU中，每个核可拥有自己的Cache，又可共用同一Cache
    + 必须采用多线程执行（真正并行）
  + 共享内存多处理器（`SMP`）概念：共享单一物理地址空间的多处理器
    + 统一存储访问（UMA）多处理器：每个处理器对所有存储单元的访问时间大致相同（与提出访问的处理器和访问位置无关）
      + 每个CPU的Cache都是共享内存中一部分副本
    + 非统一存储访问（NUMA）多处理器：某些存储器访存更快
      + 访存需经北桥（内存控制，与内存相连）





#### 第四章 文件管理

+ 文件：以硬盘为载体存储在计算机上的信息集合
  + 用户进行输入输出时，**以文件为基本单位**
  + 数据项：文件系统最低级数据组织形式
    + 基本数据项：描述一个对象某种属性的一个值（数据中**最小逻辑单位**）
    + 组合数据项（多个基本数据项组成）
  + 记录：描述一个对象某方面属性
  + 文件：创建者所定义、具有文件名的一组相关元素集合
    + 结构文件：若干相似记录组成
    + 无结构文件：字符流（二进制文件或字符文件）

  + 文件属性：名称（**唯一**）、类型、创建者（ID）、所有者、位置、大小（**可包含文件允许最大值**）、保护（访问控制信息）、创建时间和最后一次修改及存取时间
  + **文件控制块**（FCB）：实现**按名存取**
    + 包含字段
      + 基本信息：**文件名、物理位置**、逻辑结构和物理结构
      + 存取控制信息
      + 使用信息




+ 文件的基本概念（P253）
  + 文件索引节点（`inode`）：文件描述信息可单独成为一个索引节点i，文件目录中每个目录项为**文件名+索引节点号（指针）**
    + 检索目录时，文件的其他描述信息不须调入内存
    + **文件描述符**：文件在被打开时，在其**打开文件表**中的索引号
      + **一旦文件被打开，文件操作就都使用文件描述符（而非文件名）实现**
  + 文件的操作：
    + 建立：分配外存给文件（大小、位置），目录内增加**目录项**
    + 删除：通过系统调用删除文件目录项和FCB，回收占用空间（**内存和外存**）
    + 打开与关闭：将目录项对应文件内容由外存复制到内存（`open`），使用`close`调用关闭
      + 系统维护了一个打开文件信息表，“打开文件表”，当用户再次访问时，返回此索引号（查找打开表内容）
      + 多个进程可以同时打开文件的操作系统（多处理机？）中，通常采用两级表（整个系统表和每个进程表）
        + 前者打开文件表包含与进程无关信息（文件在磁盘位置、访问时间等外部属性）
          + 并关联一个**打开计数器**，记录多少进程打开此文件，直至为0时才从此表删除此条目
        + 后者打开文件表保存进程对文件使用信息（文件当前读写指针、文件访问权限）
      + 每个打开文件都具有关联信息：当前文件位置指针（内存）、文件打开计数、文件磁盘位置、访问权限
    + 读：找到目录项后，目录项内另一指针执行读操作
    + 写：相比读，还需要将内容写回外存
  + 文件的保护：
    + 访问类型：读、写、执行、添加（末尾添加）、删除和列表清单（列出文件名和相关属性）
    + 分类：
      + 口令保护
      + 加密保护
      + 访问控制：由ACL设置用户（拥有者、组【共享】、其他）及其所允许访问类型（二维表，每项都为0或1控制）

  

  + **文件逻辑结构**
    + 无结构文件：（最简单）字符流组成
    + 有结构文件（记录式）：定长记录（记录长度相同）与变长记录（**只能顺序查找**）
      + 顺序文件（顺序存储或链式存储）：按记录排列方式分
        + 串结构：记录顺序和关键字无关
        + 顺序结构：记录按关键字顺序排列（定长可折半）
      + 索引文件：索引表按关键字排序（本身也是定长顺序文件）【用户建立】
      + 索引顺序文件：将记录分组（组内无序，组间有序），分块查找
      + 直接文件或散列文件：由给定记录键值对应散列决定记录**物理地址**
  + **文件物理结构**（空闲磁盘块管理）
    + 连续分配：每个文件在磁盘上占有连续块，会产生外部碎片
    + 链接分配
      + 隐式链接：每个磁盘块都有指向下一磁盘块的指针（对用户透明），增加了内部碎片【仅顺序】
      + 显式链接：整个磁盘内设置仅一张**文件分配表（FAT）**，每个表项存放指向下一盘块的指针（盘块号）
    + 索引分配：将每个文件的所有盘块号集中放在一个表中
      + 思想：当访问某一文件时，没必要将FAT整个调入内存，事实上只需要将其对应的盘块号调入；
      + 单级索引分配：为每个文件分配一个索引表，该表记录分配给该文件对应的物理块号
      + 多级索引分配：文件太大，导致表内容太多时，使用多级索引来索引该索引表
      + 混合索引分配：为了适应多种文件大小，对**小文件**采用**直接寻址**，中大型采用多级索引



+ 目录（P280）
  + 目录概念：FCB的有序集合，一个FCB就是一个文件目录项
  + 树形目录
    + 文件路径名是字符串（根目录出发->绝对路径）
  + 目录的操作
    + 搜索
    + 创建文件
    + 删除文件：两种方式
      + 不删除非空目录（删除时要先删除目录中所有文件，**递归**删除子目录）
      + 可删除非空目录（目录中文件和子目录同时被删除）
    + 显示目录：请求显示目录内容（文件及属性）
    + 修改目录：目录项（文件）属性变化（移动）
  + 硬链接和软链接
    + 硬链接：基于索引节点共享方式，不同用户访问同个文件时，**都有指向索引节点**（其中有引用计数记录用户数）
      + 当`count=0`时才删除此文件
    + 软链接：符号链实现文件共享（类似快捷方式）
      + 只有文件主拥有**指向其索引节点**指针【物理块】，其他用户只能根据其中记录的路径名去查询文件【**只能找到目录项**】



+ 文件系统
  + 文件系统的全局结构（`layout`）
    + I/O控制层：设备驱动程序和中断处理程序，在内存和磁盘系统之间传输信息
    + 基本文件系统：通过向对应设备驱动程序发送信息来进行对应操作
    + 文件组织模块：将文件逻辑块转换为物理块地址（包括空闲空间管理器）
    + 逻辑文件系统：管理文件的外部属性信息（还负责文件保护）
  + 文件系统在外存中的结构（P293）
    + 主引导记录（MBR）：0号扇区（之后是分区表）
    + 引导块：
    + 超级块：
    + 文件系统空闲块信息：
  + 文件系统在内存中的结构
    + 内存中的安装表
    + 内存中的目录结构缓存
    + 整个系统的打开文件表
    + 每个进程的打开文件表
  + 外存空闲空间管理办法
  + 虚拟文件系统
  + 文件系统挂载（`mounting`）



---



#### 第六章 总线

+ 总线的基本概念



+ 总线的组成及性能指标
+ 总线事务和定时





#### 第七章 输入/输出系统

+ I/O接口（I/O控制器）
  + I/O功能
  + 基本结构
  + 端口
  + 编址



+ I/O方式
  + 程序控制方式
  + 程序中断方式
    + 中断基本概念
    + 中断响应过程
    + 中断处理过程
    + 多重中断概念
    + 中断屏蔽概念
  + DMA方式：
    + DMA控制器组成
    + DMA传送过程



#### 第五章 输入/输出管理

+ I/O管理基础
  + 设备
    + 概念
    + 分类
    + I/O接口
  + I/O控制方式
    + 轮询方式
    + 中断方式
    + DMA方式
  + I/O软件层次结构
    + 中断处理程序
    + 驱动程序
    + 设备独立性软件
    + 用户层I/O软件
  + 输入输出应用程序接口
    + 字符设备接口
    + 块设备接口
    + 网络设备接口
    + 阻塞/非阻塞I/O



+ 设备独立软件
  + 缓冲区管理
    + 设备分配与回收
    + 假脱机技术（`SPOOLing`）
    + 设备驱动程序接口



+ 外存管理
  + 磁盘
    + 磁盘结构
    + 格式化
    + 分区
    + 磁盘调度算法
  + 固态硬盘
    + 读/写性能特效
    + 磨损均衡