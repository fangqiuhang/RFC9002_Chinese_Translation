---
title: "6.1. 基于确认的检测"
anchor: "6.1_Acknowledgment-Based_Detection"
weight: 6100
rank: "h2"
---

基于确认的丢包检测吸收了TCP的快速重传（详见《[RFC5681](https://www.rfc-editor.org/info/rfc5681)》）、早期重传（详见《[RFC5827](https://www.rfc-editor.org/info/rfc5827)》）、前向确认（详见《[FACK](https://doi.org/10.1145/248157.248181)》）、SACK丢包恢复（详见《[RFC6675](https://www.rfc-editor.org/info/rfc6675)》）和RACK-TLP（详见《[RFC8985](https://www.rfc-editor.org/info/rfc8985)》）的思想。本节概述了这些算法在QUIC中是如何实现的。

如果数据包满足了所有以下条件，那么它会被认定为丢包：

* 该数据包处于未被确认和在途的状态，并且发送时间早于某已被确认的数据包。

* 该数据包的发送顺序比某已被确认的数据包还要早`kPacketThreshold`个数据包（详见[第6.1.1章](#6.1.1_Packet_Threshold)），或距离其发送已经过去足够久的时间（详见[第6.1.2章](#6.1.2_Time_Threshold)）。

确认能表明某个后发送的数据包已经被接收到，而数据包数量阈值和数据包发送时间阈值为数据包乱序提供了一定的容忍度。

将数据包错误地认定为丢包会导致不必要的重传，并有可能因为拥塞控制器在检测到丢失时的行为而产生性能上的损失。QUIC实现可以检测到无效重传，然后提高针对乱序的数据包数量阈值或数据包发送时间阈值来减少将来的无效重传和错误的丢包事件。具有自适应的时间阈值的QUIC实现{{< req_level MAY >}}选择以较小的初始乱序阈值来启动，以最小化恢复延迟。
