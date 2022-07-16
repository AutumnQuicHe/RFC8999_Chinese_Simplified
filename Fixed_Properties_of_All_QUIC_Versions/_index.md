---
title: "2. 所有QUIC版本之间保持不变的属性"
anchor: "2_Fixed_Properties_of_All_QUIC_Versions"
weight: 200
---

除了提供安全、多路复用的传输功能，QUIC《[QUIC协议](/RFC9000_Chinese_Translation)》还支持版本协商。
这将使得协议能够在以后的岁月中为适应新的需求而更新，而协议的诸多特性可以随着版本的迭代而不断改变。

本文阐述QUIC的一些在新的QUIC版本开发及部署的过程中依旧保持不变的属性。
所有这些不变属性都与IP版本无关。

本文的主要目标是确保后续QUIC新版本的迭代。
通过陈述QUIC的这些不可更改的属性，本文试图维持QUIC终端对QUIC协议任何其他方面的改动进行协商的能力。
因此，这也保证了暴露到一条QUIC连接两个终端之外的信息量最少。QUIC协议在本文明确禁止之外的任何方面，都是可以在不同版本之间修改的。

[附录A](#Appendix_A_Incorrect_Assumptions)包含一份非详尽的清单，列出了一些基于对QUIC版本1的了解可能做出的不正确的猜想，这些不适用于QUIC的任何版本。