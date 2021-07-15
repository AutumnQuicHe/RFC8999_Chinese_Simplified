---
title: "6. 版本协商"
anchor: "6_Version_Negotiation"
weight: 600
---

一个QUIC终端收到一个有长包头的数据包及一个版本其不能理解或不支持的话，就可能回复一个版本协商包。短包头数据包不会触发版本协商。

一个版本协商包设置上首个字节的高位，也就是说它是一个[第5.1章]()定义的长包头数据包。一个版本协商包可以通过其版本字段识别，因为这个字段会被设置为0x00000000。

[图4](#Figure_4_Version_Negotiation_Packet)是一个示例结构：


{{% block_ref
    indx="Figure_4_Version_Negotiation_Packet"
    title="图4：版本协商包" %}}
```
版本协商包 {
  Header Form (1) = 1,
  Unused (7),
  Version (32) = 0,
  Destination Connection ID Length (8),
  Destination Connection ID (0..2040),
  Source Connection ID Length (8),
  Source Connection ID (0..2040),
  Supported Version (32) ...,
}
```
{{% /block_ref %}}

一个版本协商包只有首字节最重要的那个比特位有着任意定义的值。其剩余的7个比特位标记为“未使用”，在发送的时候可以被设置为任意值，且 {{< req_level MUST >}} 被接收端忽略。

在源连接ID字段后面，版本协商包包涵一个支持版本字段列表，每个字段标识一个终端能够支持的版本（也就是客户端支持的QUIC版本的版本号挨个列下去）。一个版本协商包不包含其他字段，一个终端 {{< req_level MUST >}} 忽略没有支持版本字段或包含一个不完全的版本值的包。

版本协商包不使用完全的或加密的保护。某些特定的QUIC版本可能包含准许终端鉴别支持版本列表里的值是否存在修改或损坏的协议手段。

一个终端 {{< req_level MUST >}} 在其目标连接ID字段包含它收到的数据包的源连接ID值。{{< req_level MUST >}} 将收到数据包的目标连接ID字段值复制给源连接ID字段，该值是客户端随机产生的。回显两个连接ID给客户端一些保证，表明服务端收到了包，且版本协商包不是由对其不可见的攻击者生成的。

终端收到版本协商包后，可以在随后的数据包中更改QUIC版本。终端更改QUIC版本的条件将取决于其选择的版本。

《[QUIC协议]()》详细描述了支持QUIC版本1的终端如何创建和处理一个版本协商包。
