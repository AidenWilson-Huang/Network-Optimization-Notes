# WinPcap

*WinPcap是Windows平台下访问网络数据链路层的开源库 ， 该库已达到工业标准的应用要求。WinPcap允许应用程序绕开网络协议栈来捕获与传递网络数据包，并具有额外的有用特性，包括内核层的数据包过滤、一个 网络统计引擎与支持远程数据包捕获。*

## WinPcap简介

###  什么是 *WinPcap*

大多数网络应用程序通过被广泛使用的操作系统原语来访 问网络，诸如*sockets。操作系统已经处理了底层的细节问题（如协议处理，数据包的封装等），并提供与读写文 件类似的、熟悉的接口，这使得用该方法可以很容易的访问网络中的数据。*

然而有些时候，这种*“简单的方式”并不能满足任务要求，因为有些应用程序需要直接访问网络中的数据包。也就是说，应用程序需要访问网络中的“原 始”数据包，即没有被操作系统使用网络协议进行处理过的数据包。*

*WinPcap的目的就是为Win32应用程序提供这种访问方式。WinPcap提供下列功能：*

- 捕获原始 数据包，无论是发送到运行*WinPcap机器上的数据包，还是在其它主机（* 共享介质 ）上进行交换的数据包
- 在数据包 分派给应用程序前，根据用户指定的规则过滤数据包
- 将原始数 据包发送到网络
- 收集网络流量的统计信息

### *WinPcap* 的优点

***\*自由\**** *WinPcap遵 循[BSD open source licence ](http://www.winpcap.org/misc/copyright.htm)发布。这意味着 你的应用程序拥 有全部自由来修改与使用它 ，即使应用程序是商业化的。*

***\*高性能\**** *WinPcap实现了有关数据包 捕获文献中描述的所有典型的优化方法（比如内核级的过滤与缓冲，减少上下文交换，数据包部分内容复制），加上一些原创的优化方法，如JIT过滤器编辑（JIT filter compilation） 与内核级的统计过程。因为这 些原因，WinPcap胜过其它可比的方法。*

***\*普及\**** *WinPcap被 许多工具作为网络接口使用——无论是自由软件还是商业软件。包括网络协议分析器、网络监视器、网络入侵检测系统、网络嗅探器、网络流量生成器、网络测试器 等等。如[Wireshark ](http://www.wireshark.org/)、[Nmap ](http://www.insecure.org/nmap/)、 [Snort ](http://www.snort.org/)、[WinDump ](http://www.winpcap.org/windump)、[ntop ](http://www.ntop.org/)这些工具，在网络社群中是众所周知的。WinPcap每天被下载上千 次。*

***\*测试充分与可信赖\**** 许多用户对*WinPcap 在广泛的平台上的测试与发现最难以发现的缺陷做出了经年的贡献。WinPcap的开发者是富有经验的Windows驱动程序编写者，同时他们软件开发方法 的重点就是强调固若顽石(rock-solid)的稳定性。记住：一个多缺陷的驱动程序意味着蓝屏（Windows操作系统在崩溃后，屏蔽该系统所有处理 器的所有中断后，将显示器切换到低分辨率的VGA图形模式下，绘制一个蓝色背景，然后显示停止码，后面紧跟着一些文本信息来建议用户应该怎么办的画面）。*

***\*最终用户易于使用\**** *WinPcap作为单个小的可执 行文件发布，可运行在每个所支持的操作系统上。开始使用这个可执行文件后，Windows就能捕获与发送原始数据包。不可能再有更简单的操作了。*

***\*程序员易于使用\**** 每个版本的*WinPcap 带有一个开发者包([developer's pack](http://www.winpcap.org/install/default.htm) )，包括文档、库与include文件，是你立即开发应用程序所必需的。开发者包还包含一个示例程序集，可用Visual Studio或Cygnus编译，用来作为一个极好的起点。*

***\*多平台\**** *WinPcap在Windows NT、Windows 2000、Windows XP与Windows Server 2003平台上被积极地维护。WinPcap也能工作在Windows 95、Windows 98 与Windows ME平台上，但在这些操作系统上将不再维护。对Windows Vista具有初步的支持，但有一些特性并不具备。*

***\*可移植\**** *WinPcap与libpcap 具有完全的兼容性。这意味着能够使用它移植已在Unix或Linux下存在的工具到Windows下。这也意味着Windows应用程序可以很容易的移植 到Unix下使用。*

***\*良好的文档\**** *WinPcap手册用一种容易理 解的超文本链接方式描述，对API与内部进行了文档化。该文档包含一个指南，让你一步一步地熟悉WinPcap的所有特性。*

***\*商业化支持\**** 如果你对专业的*WinPcap 支持感兴趣、或当一些事情出错时你需要一个电话号码寻求帮助，或者在开发底层网络代码时需要帮助，* *[CACE Technologies（ http://www.cacetech.com/support ）可以帮助你 ](http://www.cacetech.com/support)。*

### 哪类程序使用了 *WinPcap*

*WinPcap可被许多类型的网络工具使用，比如具有分析，解决纷争，安全和监视功能的工具。特别地，一些基于WinPcap 的典型工具如下所示：*

- 网络与协 议分析器 *(network and protocol analyzers)*
- 网络监视 器 *(network monitors)*
- 网络流量 记录器 *(traffic loggers)*
- 网络流量 生成器 *(traffic generators)*
- 用户层网 桥及路由 *(user-level bridges and routers)*
- 网络入侵 检测系统 *(network intrusion detection systems (NIDS))*
- 网络扫描 器 *(network scanners)*
- 网络安全 工具 *(security tools)*

### 什么是 *WinPcap* 不能做的

*WinPcap独立 于诸如 TCP-IP协议的主机协议来发送和接收网络数据包。这意味着WinPcap不能阻塞、过滤或操纵同一机器上其它应用程序的通信。它只是简单地"嗅探"网 络上所传输的数据包，因此WinPcap不能提供诸如网络流量控制、服务质量调度和个人防火墙之类的功能支持。*



## 网络分析与嗅探的基础知识

**网络分析** (Network analysis) (也称为网络流量分析、协议分析、嗅探、数据包分析、窃听，等等)就是通过捕获网络流量并深入检查，来决定网络中发生了什么情况的过程。一个网络分析器对 通用协议的数据包进行解码，并以可读的格式显示网络流量的内容。 **嗅探器** （ *sniffer* ）是一种监视网络上所传输数据的程 序。未经授权的嗅探器对网络安全构成威胁，因为它们很难被发现并且可在任何地方被插入，这使得它们成为黑客最喜欢使用的一种工具。

网 络分析器之间的差别，在于诸如支持能解码的协议数量、用户接口、图形化与统计能力等主要特性的不同。其它的差别还包括了推理能力（比如，专家分析特性）与 数据包解码的质量。尽管几个不同的网络分析器针对同一个协议进行解码，但在实际环境中可能其中的一些会比另外一些工作得更好。

图 2-1为Wireshark网络分析器的显示窗口。一个典型的网络分析器用三个窗格显示所捕获的网络流量：

![img](http://img1.51cto.com/attachment/200909/10/918801_1252580814XJTc.gif)

**图2-1** **Wireshark网络分析器的显示窗口**

**概要** 该窗格对所捕 获的内容显示一行概要。包含日期、时间、源地址、目标地址、与最高层协议的名字与信息字段。

**详情** 该窗格提供所 捕获数据包所包含的每层细节信息（采用树形结构）。

**数据** 该窗格用十六进制与文本格式显示原始的被捕获数据。

一个网络分析器是由硬件与软件共同组成。可以是一个带有特定软件的单独硬件设备，或者是安装在台式电脑或膝上电脑之上的一个软件。尽管每种 产品之间具有差别，但都是由下列五个基本部分组成。

**硬件** 多数网络分析器是基于软件的，并工作于 标准的操作系统与网卡之上。然而，一些硬件网络分析器提供额外的功能，诸如分析硬件故障（比如循环冗余纠错（CRC）错误、电压问题、网线问题、抖动、逾 限（jabber）、协商错误等等）。一些网络分析器仅支持以太网或无线网适配器，而其它的可支持多重适配器，并允许用户定制它们的配置。依据实际情况， 可能也需要一个集线器或一个网线探针（cable tap）连接已有的网线。

**捕获驱动器** 这是网络分析器中负责 从网线上捕获原始网络流量的部分。它滤出了所需保持的流量，并把所捕的获数据保存在一个缓冲区中。这是网络分析器的核心——没有它就无法捕获数据。

**缓冲区** 该组件存储所捕获的数据。数据能够被存入一个缓冲区中只到该缓冲区被填满为止，或者采用循环缓冲的方式，那么最新的 数据将会替换最旧的数据。采用磁盘或内存均可实现缓冲区。

**实时分析** 当数据一离开网线，该特性就可对数据执行分 析。一些网络分析器利用该特性发现网络性能问题、同时网络入侵检测系统利用它寻找入侵活动。

**解码(器)** 该组件显示网络流量的内容（带有描述），所以是可读的 。解码是特定于每个协议的，因此网络分析器当前支持可解码的协议数目是变化的，网络分析器可能经常加入新的解码。





# Wireshark

## 简介

WireShark是非常流行的网络封包分析工具，可以截取各种网络数据包，并显示数据包详细信息。常用于开发测试过程中各种问题定位。本文主要内容包括：
1、Wireshark软件下载和安装以及Wireshark主界面介绍。

2、WireShark简单抓包示例。通过该例子学会怎么抓包以及如何简单查看分析数据包内容。

3、Wireshark过滤器使用。通过过滤器可以筛选出想要分析的内容。包括按照协议过滤、端口和主机名过滤、数据包内容过滤。



## Wireshark 开始抓包示例

先介绍一个使用wireshark工具抓取ping命令操作的示例，让读者可以先上手操作感受一下抓包的具体过程。
1、打开wireshark 2.6.5，主界面如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124120704182.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
2、选择对应的网卡，右键，会出现Start Capture(开始捕获)，点击即可进行捕获该网络信息，开始抓取网络包
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124120915674.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)3、执行需要抓包的操作，如ping www.baidu.com。
4、操作完成后相关数据包就抓取到了。为避免其他无用的数据包影响分析，可以通过在过滤栏设置过滤条件进行数据包列表过滤，获取结果如下。
说明：ip.addr == 180.101.49.11 and icmp 表示只显示ICPM协议且源主机IP或者目的主机IP为119.75.217.26的数据包。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124007777.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124035735.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
5、wireshark抓包完成，就这么简单。关于wireshark过滤条件和如何查看数据包中的详细内容在后面介绍。

### WireShark抓包界面

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124122697.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
说明：数据包列表区中不同的协议使用了不同的颜色区分。协议颜色标识定位在菜单栏View --> Coloring Rules。如下所示
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124209888.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)

**WireShark 主要分为这几个界面**

1、Display Filter(显示过滤器)， 用于设置过滤条件进行数据包列表过滤。菜单路径：Analyze --> Display Filters。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124434536.png)2、Packet List Pane(数据包列表)， 显示捕获到的数据包，每个数据包包含编号，时间截，源地址，目标地址，协议，长度，以及数据包信息。 不同协议的数据包使用了不同的颜色区分显示。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124547661.png)
3、Packet Details Pane(数据包详细信息), 在数据包列表中选择指定数据包，在数据包详细信息中会显示数据包的所有详细信息内容。**数据包详细信息面板是最重要的，用来查看协议中的每一个字段**。各行信息分别为
（1）Frame: 物理层的数据帧概况

（2）Ethernet II: 数据链路层以太网帧头部信息

（3）Internet Protocol Version 4: 互联网层IP包头部信息

（4）Transmission Control Protocol: 传输层T的数据段头部信息，此处是TCP

（5）Hypertext Transfer Protocol: 应用层的信息，此处是HTTP协议
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124801282.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)

### TCP包的具体内容

从下图可以看到wireshark捕获到的TCP包中的每个字段。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124124945729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)

4. Dissector Pane(数据包字节区)。

## Wireshark过滤器设置

初学者使用wireshark时，将会得到大量的冗余数据包列表，以至于很难找到自己自己抓取的数据包部分。wireshar工具中自带了两种类型的过滤器，学会使用这两种过滤器会帮助我们在大量的数据中迅速找到我们需要的信息。
（1）抓包过滤器

捕获过滤器的菜单栏路径为Capture --> Capture Filters。**用于在抓取数据包前设置。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124125128229.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)如何使用？可以在抓取数据包前设置如下。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124125917381.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
ip host 60.207.246.216 and icmp表示只捕获主机IP为60.207.246.216的ICMP数据包。获取结果如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124125937208.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)（2）显示过滤器
显示过滤器是用于在抓取数据包后设置过滤条件进行过滤数据包。通常是在抓取数据包时设置条件相对宽泛，抓取的数据包内容较多时使用显示过滤器设置条件过滤以方便分析。同样上述场景，在捕获时未设置捕获规则直接通过网卡进行抓取所有数据包，如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124130405245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)执行ping www.huawei.com获取的数据包列表如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124130422459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
观察上述获取的数据包列表，含有大量的无效数据。这时可以通过设置显示器过滤条件进行提取分析信息。ip.addr == 211.162.2.183 and icmp。并进行过滤。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124130446233.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)上述介绍了抓包过滤器和显示过滤器的基本使用方法。**在组网不复杂或者流量不大情况下，使用显示器过滤器进行抓包后处理就可以满足我们使用**。下面介绍一下两者间的语法以及它们的区别。

## wireshark过滤器表达式的规则

1、抓包过滤器语法和实例

抓包过滤器类型Type（host、net、port）、方向Dir（src、dst）、协议Proto（ether、ip、tcp、udp、http、icmp、ftp等）、逻辑运算符（&& 与、|| 或、！非）

（1）协议过滤

比较简单，直接在抓包过滤框中直接输入协议名即可。

TCP，只显示TCP协议的数据包列表

HTTP，只查看HTTP协议的数据包列表

ICMP，只显示ICMP协议的数据包列表

（2）IP过滤

host 192.168.1.104

src host 192.168.1.104

dst host 192.168.1.104

（3）端口过滤

port 80

src port 80

dst port 80

（4）逻辑运算符&& 与、|| 或、！非

src host 192.168.1.104 && dst port 80 抓取主机地址为192.168.1.80、目的端口为80的数据包

host 192.168.1.104 || host 192.168.1.102 抓取主机为192.168.1.104或者192.168.1.102的数据包

！broadcast 不抓取广播数据包
2、显示过滤器语法和实例

（1）比较操作符

比较操作符有== 等于、！= 不等于、> 大于、< 小于、>= 大于等于、<=小于等于。

（2）协议过滤

比较简单，直接在Filter框中直接输入协议名即可。**注意：协议名称需要输入小写。**

tcp，只显示TCP协议的数据包列表

http，只查看HTTP协议的数据包列表

icmp，只显示ICMP协议的数据包列表
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124130859675.png)
（3） ip过滤
ip.src ==192.168.1.104 显示源地址为192.168.1.104的数据包列表

ip.dst==192.168.1.104, 显示目标地址为192.168.1.104的数据包列表

ip.addr == 192.168.1.104 显示源IP地址或目标IP地址为192.168.1.104的数据包列表

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124131106351.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)（4）端口过滤

tcp.port ==80, 显示源主机或者目的主机端口为80的数据包列表。

tcp.srcport == 80, 只显示TCP协议的源主机端口为80的数据包列表。

tcp.dstport == 80，只显示TCP协议的目的主机端口为80的数据包列表。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124131139111.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)（5） Http模式过滤

http.request.method==“GET”, 只显示HTTP GET方法的。
（6）逻辑运算符为 and/or/not

过滤多个条件组合时，使用and/or。比如获取IP地址为192.168.1.104的ICMP数据包表达式为ip.addr == 192.168.1.104 and icmp
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124131246646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)（7）按照数据包内容过滤。假设我要以IMCP层中的内容进行过滤，可以单击选中界面中的码流，在下方进行选中数据。如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124131458129.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
右键单击选中后出现如下界面（作为过滤器应用）
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124131650672.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)选中Select后在过滤器中显示如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124131720526.png)
后面条件表达式就需要自己填写。如下我想过滤出data数据包中包含"abcd"内容的数据流。**包含的关键词是contains 后面跟上内容。**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124131801917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)看到这， 基本上对wireshak有了初步了解。

### Wireshark抓包分析TCP[三次握手](https://so.csdn.net/so/search?q=三次握手&spm=1001.2101.3001.7020)

（1）TCP三次握手连接建立过程

第一步：客户端发送一个SYN=1，ACK=0标志的数据包给服务端，请求进行连接，这是第一次握手；

第二步：服务端收到请求并且允许连接的话，就会发送一个SYN=1，ACK=1标志的数据包给发送端，告诉它，可以通讯了，并且让客户端发送一个确认数据包，这是第二次握手；

第三步：服务端发送一个SYN=0，ACK=1的数据包给客户端，告诉它连接已被确认，这就是第三次握手。TCP连接建立，开始通讯。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132105773.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
（2）wireshark抓包获取访问指定服务端数据包
Step1：启动wireshark抓包，打开浏览器输入www.huawei.com。

Step2：使用ping www.huawei.com获取IP。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132204943.png)
Step3：输入过滤条件获取待分析数据包列表 ip.addr == 211.162.2.183

![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132228153.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70) 图中可以看到wireshark截获到了三次握手的三个数据包。第四个包才是HTTP的， 这说明HTTP的确是使用TCP建立连接的。

第一次握手数据包

客户端发送一个TCP，标志位为SYN，序列号为0， 代表客户端请求建立连接。 如下图。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132401203.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)数据包的关键属性如下：

SYN ：标志位，表示请求建立连接

Seq = 0 ：初始建立连接值为0，数据包的相对序列号从0开始，表示当前还没有发送数据

Ack =0：初始建立连接值为0，已经收到包的数量，表示当前没有接收到数据
第二次握手的数据包

服务器发回确认包, 标志位为 SYN,ACK. 将确认序号(Acknowledgement Number)设置为客户的I S N加1，即0+1=1, 如下图
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021012413260667.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)数据包的关键属性如下：

Seq = 0 ：初始建立值为0，表示当前还没有发送数据

Ack = 1：表示当前端成功接收的数据位数，虽然客户端没有发送任何有效数据，确认号还是被加1，因为包含SYN或FIN标志位。（并不会对有效数据的计数产生影响，因为含有SYN或FIN标志位的包并不携带有效数据）

第三次握手的数据包

客户端再次发送确认包(ACK) SYN标志位为0,ACK标志位为1.并且把服务器发来ACK的序号字段+1,放在确定字段中发送给对方.并且在数据段放写ISN的+1, 如下图:
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132839271.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)
数据包的关键属性如下：

ACK ：标志位，表示已经收到记录

Seq = 1 ：表示当前已经发送1个数据

Ack = 1 : 表示当前端成功接收的数据位数，虽然服务端没有发送任何有效数据，确认号还是被加1，因为包含SYN或FIN标志位（并不会对有效数据的计数产生影响，因为含有SYN或FIN标志位的包并不携带有效数据)。

就这样通过了TCP三次握手，建立了连接。开始进行数据交互
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132908250.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)下面针对数据交互过程的数据包进行一些说明：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132930436.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)数据包的关键属性说明

Seq: 1

Ack: 1: 说明现在共收到1字节数据
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124132947574.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)Seq: 1
Ack: 951: 说明现在服务端共收到951字节数据

在TCP层，有个FLAGS字段，这个字段有以下几个标识：SYN, FIN, ACK, PSH, RST, URG。如下
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124133013316.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3p6d3doaHBw,size_16,color_FFFFFF,t_70)其中，对于我们日常的分析有用的就是前面的五个字段。它们的含义是：SYN表示建立连接，FIN表示关闭连接，ACK表示响应，PSH表示有DATA数据传输，RST表示连接重置。

## Wireshark分析常用操作

调整数据包列表中时间截显示格式。调整方法为View -->Time Display Format --> Date and Time of Day。调整后格式如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210124133141945.png)





# Virtual Box

一款开源跨平台虚拟化软件，使用该软件，开发人员能够在一台设备上运行多个操作系统。