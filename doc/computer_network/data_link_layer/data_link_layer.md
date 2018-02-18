# 数据链路层
## 封装成帧
* 在一段数据前后分别添加首部和尾部
* 帧的数据部分的长度上限--最大传送单元MTU（Maximum Transfer Unit）
* 帧开始符SOH，帧结束符EOT
* 出现传输差错：帧丢失、帧重复、帧失序，因此，可以增加：帧编号、确认和重传机制

## 点对点协议 PPP
* 需要支持
    * 封装成帧；
    * 差错检测；
    * 检测连接状态；
    * 最大传送单元；

## 局域网的数据链路层
* 拆成两个子层，即：逻辑链路控制LLC（Logical Link Control）子层和媒体接入控制MAC（Medium Access Control）子层

## CSMA/CD 协议
* 载波监听多点接入/碰撞检测（Carrier Sense Multiple Access with Collision Detection）
* 协议的实质是“载波监听”和“碰撞检测”
* 载波监听：即：发送前先监听，是否有其他站在发送数据
* 碰撞检测：即：边发送边监听

## 三种帧
* 单播（unicast）帧：一对一
* 广播（broadcast）帧：一对全体
* 多播（multicast）帧：一对多

## 虚拟局域网VLAN（Virtual LAN）
* 由一些局域网网段构成的与物理位置无关的逻辑组

[返回目录](../CONTENTS.md)