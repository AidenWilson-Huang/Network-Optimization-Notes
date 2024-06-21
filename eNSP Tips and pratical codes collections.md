#### 文章目录

- [一、同一交换机下的PC通信](https://blog.csdn.net/m0_46085118/article/details/131224141#PC_1)
- [二、不交换机下的PC通信](https://blog.csdn.net/m0_46085118/article/details/131224141#PC_21)
- [三、配置静态路由通信](https://blog.csdn.net/m0_46085118/article/details/131224141#_42)
- [四、路由器rip协议配置](https://blog.csdn.net/m0_46085118/article/details/131224141#rip_88)
- [五、路由器ospf协议配置](https://blog.csdn.net/m0_46085118/article/details/131224141#ospf_140)
- [六、单臂路由](https://blog.csdn.net/m0_46085118/article/details/131224141#_195)
- [七、通过三层交换机使不同的Vlan能连通](https://blog.csdn.net/m0_46085118/article/details/131224141#Vlan_258)
- [八、设备console密码模式](https://blog.csdn.net/m0_46085118/article/details/131224141#console_302)
- [九、设备console用户密码模式（AAA模式）](https://blog.csdn.net/m0_46085118/article/details/131224141#consoleAAA_326)
- [十、Telnet控制模式，通过路由器控制旁边的路由器](https://blog.csdn.net/m0_46085118/article/details/131224141#Telnet_348)
- [十一、路由器配置DHCP](https://blog.csdn.net/m0_46085118/article/details/131224141#DHCP_385)
- [十二、链路聚合](https://blog.csdn.net/m0_46085118/article/details/131224141#_421)
- [参考文档](https://blog.csdn.net/m0_46085118/article/details/131224141#_458)



## 一、同一交换机下的PC通信

- 因为直接启动交换机，交换机上的两端端口默认Vlan都为1，所以什么都不用配置直接就能通信。同时注意，两台PC机要在同一个网段下（ip地址+掩码即可得到网段）
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/63be83ecd4ff4033a6f3bd7bbdf0e54d.png)
- 主要涉及的命令（用于参考）

```shell
#进入命令行控制模式
system-view
# 对设备命名
sysname coreswitch1
# 创建VLAN
vlan 2
quit 
# 将端口指定到VLAN中
interface GigabitEthernet 0/0/1
port link-type access
port default vlan 2
quit
123456789101112
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/1c27ab3409804d21ba06d457d7d6f6bb.png)

## 二、不交换机下的PC通信

- 因为直接启动交换机，交换机上的两端端口默认Vlan都为1，所以什么都不用配置直接就能通信。
- 图上4个电脑都相互能ping通

![在这里插入图片描述](https://img-blog.csdnimg.cn/9cdddec65da74425bbb52c747736a77b.png)

- 如下图PC1不能和PC2通信，PC1能和PC3通信，PC2不能和PC4通信
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/cabc6639ab8e4c3bbef2f845a66eb760.png)
- 如下图PC1不能和PC2通信，PC1能和PC3通信，PC2能和PC4通信
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/82b0b12703c348c3a936f5509750edf6.png)
- 涉及的命令（用于参考）

```shell
# 创建端口组1，把端口1到端口10都加入到端口组中，然后把组1中的端口都加入到Vlan2中
port-group 1
group-member GigabitEthernet0/0/1 to GigabitEthernet 0/0/10
port link-type access
# vlan2不能不存在（不存在则创建），不然会报错
port default vlan 2
quit
1234567
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/3b450057b6074496b6ad6297a0da1cad.png)

## 三、配置静态路由通信

- 最后配置形成的拓扑图，本实验路由器选择的是AR2220
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/90638af9ba454ad89452bdf385b958b2.png)
- 每个设备需要运行的命令（可直接复制执行）
- AR1

```shell
system-view
sysname R1
#进入端口
interface GigabitEthernet 0/0/1
#配置端口ip地址
ip address 192.168.1.254 24
quit
interface GigabitEthernet 0/0/0
ip address 192.168.2.1 24
quit
#配置静态路由
ip route-static 192.168.3.0 24 192.168.2.2
123456789101112
```

- AR2

```shell
system-view
sysname R2
interface GigabitEthernet 0/0/1
ip address 192.168.3.254 24
quit
interface GigabitEthernet 0/0/0
ip address 192.168.2.2 24
quit
#配置静态路由
ip route-static 192.168.1.0 24 192.168.2.1
12345678910
```

- 各个设备的运行截图
  - PC1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/69efdb6903f64fbcb8e59a54211b2384.png)
  - PC2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/f50e5d72be56427ba55cc5d554781ef5.png)
  - AR1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/b874dad4cfc34e66b07a53f6159c67b2.png)
  - AR2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/f91c7a0b843845cd898cdcef68336345.png)
- 运行成功
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/8df2ac9a4a2044639eb359fe12117ab4.png)

## 四、路由器rip协议配置

- 最后配置形成的[拓扑图](https://so.csdn.net/so/search?q=拓扑图&spm=1001.2101.3001.7020)
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/09b77a62e3da43cc8e765ec60c2bfbba.png)
- 每个设备需要运行的命令（可直接复制执行）
- AR1

```shell
system-view
sysname R1
interface GigabitEthernet 0/0/1
ip address 192.168.1.254 24
quit
interface GigabitEthernet 0/0/0
ip address 192.168.2.1 24
quit
#动态路由配置
#数字表示进程号
rip 1
network 192.168.1.0
network 192.168.2.0
quit
1234567891011121314
```

- AR2

```shell
system-view
sysname R2
interface GigabitEthernet 0/0/1
ip address 192.168.3.254 24
quit
interface GigabitEthernet 0/0/0
ip address 192.168.2.2 24
quit
#动态路由配置
#数字表示进程号
rip 1
network 192.168.2.0
network 192.168.3.0
quit
1234567891011121314
```

- 各个设备的运行截图
  - PC1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/69efdb6903f64fbcb8e59a54211b2384.png)
  - PC2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/f50e5d72be56427ba55cc5d554781ef5.png)
  - AR1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/abab55923d34464a9cf806fc535de870.png)
  - AR2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/a89ce141a04d4a36bde87d6098b5457e.png)
- 运行成功
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/671aaab1dab446c481c4e2b350e19939.png)

## 五、路由器ospf协议配置

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/df18b43e2f4e4139b6037af7aaf4e338.png)
- 每个设备需要运行的命令（可直接复制执行）
- AR1

```shell
system-view
sysname R1
interface GigabitEthernet 0/0/1
ip address 192.168.1.254 24
quit
interface GigabitEthernet 0/0/0
ip address 192.168.2.1 24
quit
#动态路由配置
#数字表示进程号
ospf 1
#数字表示网络区域
area 0
network 192.168.1.0 0.0.0.255
area 1
network 192.168.2.0 0.0.0.255
quit
quit
123456789101112131415161718
```

- AR2

```shell
system-view
sysname R2
interface GigabitEthernet 0/0/1
ip address 192.168.3.254 24
quit
interface GigabitEthernet 0/0/0
ip address 192.168.2.2 24
quit
ospf 1
area 1
network 192.168.2.0 0.0.0.255
area 0
network 192.168.3.0 0.0.0.255
quit
quit
123456789101112131415
```

- 运行截图
  - PC1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/69efdb6903f64fbcb8e59a54211b2384.png)
  - PC2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/f50e5d72be56427ba55cc5d554781ef5.png)
  - AR1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/705593a958b647c4bc7914c28ed08a0c.png)
  - AR2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/ce4569ec27f84024bf2aff0ce233bf67.png)
- 运行成功
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/1d9c6e72ef7e47cd956fe2d37bf5808d.png)

## 六、单臂路由

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/b9863cd01e86414b8e81ca992bb50d72.png)
- 每个设备需要运行的命令（可直接复制执行）
- SW1

```shell
system-view
sysname SW1
vlan bat 10 20 30
interface GigabitEthernet 0/0/2
port link-type access
port default vlan 10
interface GigabitEthernet 0/0/3
port link-type access
port default vlan 20
interface GigabitEthernet 0/0/4
port link-type access
port default vlan 30
interface GigabitEthernet 0/0/1
#设置连接方式为trunk
port link-type trunk 
#允许所有的vlan通过
port trunk allow-pass vlan all
quit
123456789101112131415161718
```

- AR1

```shell
system-view
sysname R1
interface GigabitEthernet 0/0/0.1
ip address 192.168.1.254 24
dot1q termination vid 10
# 开启广播功能
arp broadcast enable
interface GigabitEthernet 0/0/0.2
ip address 192.168.2.254 24
#设置Vlan的ID
dot1q termination vid 20
arp broadcast enable
interface GigabitEthernet 0/0/0.3
ip address 192.168.3.254 24
dot1q termination vid 30
arp broadcast enable
12345678910111213141516
```

- 运行命令截图
  - PC1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/9b690d94b640418fa8a460a6ff005ffa.png)
  - PC2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/8eb4dacadc6b42ed875c39e3472f4cc0.png)
  - PC3
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/ed27334242aa4ee4939a28636d855085.png)
  - SW1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/5a20a1a6ad3249e58d1a1f4dadbfdda9.png)
  - AR1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/7ccc562dba624559999ebd25c2f18a09.png)
- 运行成功截图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/9a60f452b79e4438bf8811e85c995755.png)

## 七、通过三层交换机使不同的Vlan能连通

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/429afa47350e4fc8987fda7ac35d83f4.png)
- 每个设备需要运行的命令（可直接复制执行）
- SW1

```shell
system-view
sysname SW1
vlan batch 10 20
interface Vlanif 10
ip address 192.168.1.254 24
interface Vlanif 20
ip address 192.168.2.254 24
interface GigabitEthernet 0/0/1
port link-type trunk
port trunk allow-pass vlan all
quit
1234567891011
```

- SW2

```shell
system-view
sysname SW2
vlan batch 10 20
interface GigabitEthernet 0/0/1
port link-type trunk
port trunk allow-pass vlan all
interface GigabitEthernet 0/0/2
port link-type access
port default vlan 10
interface GigabitEthernet 0/0/3
port link-type access
port default vlan 20
quit
12345678910111213
```

- 运行命令截图
  - SW1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/4b70bfeeb44b400bb9622cacd217d4c0.png)
  - SW2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/f928b09f01b74ad0987a823a2d0a5524.png)
- 运行成功截图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/98b13e7288f0455895fc6758fd17f734.png)

## 八、设备console密码模式

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/9fad080ccf904d2ead1c79da6d705818.png)
- 每个设备需要运行的命令（可直接复制执行）
- R1

```shell
system-view
sysname R1
user-interface console 0
#设置密码为一二三，同时密码为密文
set authentication password cipher 123
#设置用户级别
user privilege level 3
quit
12345678
```

- 运行命令截图
  - R1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/f17dc36815cf42f89edaffbb583b426e.png)
  - PC1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/939afe77273d4d08a4fdde3a3124591c.png)
- 运行成功截图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/71612f3d6d34407f885a07e827698766.png)

## 九、设备console用户密码模式（AAA模式）

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/3ea9543092db4432bc457e74a96f6188.png)
- 每个设备需要运行的命令（可直接复制执行）
- R1

```shell
system-view
sysname R1
user-interface console 0
authentication-mode aaa
quit
aaa
local-user huawei password cipher 123
local-user huawei privilege level 3
quit
123456789
```

- 运行命令截图
  - R1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/67d98a19a5814678b1a5e88e5afaaee3.png)
  - PC1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/b0bdb152a9ba4f25b8a60c3b6061542b.png)

## 十、Telnet控制模式，通过路由器控制旁边的路由器

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/5ebffb989fd4448183b0721981af11c2.png)
- 每个设备需要运行的命令（可直接复制执行）
- R1（先运行R2的代码，因为是用R1连接R2）

```shell
system-view
sysname R1
interface GigabitEthernet 0/0/0
ip address 192.168.1.1 24
quit
quit
telnet 192.168.1.2
1234567
```

- R2

```shell
system-view
sysname R2
interface GigabitEthernet 0/0/0
ip address 192.168.1.2 24
quit
#零是开始的，四为结束的，意思为五个会话
user-interface vty 0 4
set authentication password cipher 123
user privilege level 3
quit
12345678910
```

- 运行命令截图
  - R1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/623ac54a884f4fc8aaab4f6e04026a6b.png)
  - R2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/a07f9f4c61f7491b9965ef23e6404fbb.png)
- 运行成功截图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/5934811b439c4ef1909a7b4be21fd9cb.png)

## 十一、路由器配置DHCP

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/87f29e0fa8744fdc8a38fa5f2d3ddc37.png)
- 每个设备需要运行的命令（可直接复制执行）
- R1

```shell
system-view
sysname R1
#开启
dhcp enable
#创建地址池
ip pool 1
network 192.168.1.0 mask 255.255.255.0
#配置网关
gateway-list 192.168.1.254
#排除这个区间的地址不分配
excluded-ip-address 192.168.1.2 192.168.1.253
dns-list 8.8.8.8
#定义使用周期为两天
lease day 2
quit
interface GigabitEthernet 0/0/0
ip address 192.168.1.254 24
#全局配置
dhcp select global
quit
1234567891011121314151617181920
```

- 运行命令截图
  - R1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/466077793a9d4120ac1f78c67cec968e.png)
- PC1
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/d53181dd0bb94c8da75261b0f674e23b.png)
- 运行成功截图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/3331ea6e05bc4087b74f2eb898cb435f.png)

## 十二、链路聚合

- 最后配置形成的拓扑图
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/e51a12f6e21f43f2bb94d15036256951.png)
- 每个设备需要运行的命令（可直接复制执行）
- SW1

```shell
system-view
sysname SW1
interface Eth-Trunk 1
#配置为手工方式
mode manual load-balance
#配置链路聚合的物理端口
trunkport gigabitethernet 0/0/1 to 0/0/2
port link-type trunk
port trunk allow-pass vlan all
quit
12345678910
```

- SW2

```shell
system-view
sysname SW2
interface Eth-Trunk 1
mode manual load-balance
trunkport gigabitethernet 0/0/1 to 0/0/2
port link-type trunk
port trunk allow-pass vlan all
quit
12345678
```

- 运行命令截图
  - SW1
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/a4ce6ac6e8bd42cbbe625ce59b63b8f5.png)
  - SW2
    ![在这里插入图片描述](https://img-blog.csdnimg.cn/058488e02d234fc5b0ed7c1820fe9a1f.png)
- 运行成功截图
