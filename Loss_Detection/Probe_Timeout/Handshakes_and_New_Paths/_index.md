---
title: "6.2.2. 握手与新路径"
anchor: "6.2.2_Handshakes_and_New_Paths"
weight: 6220
rank: "h3"
---

在相同的网络路径上恢复出来的连接{{< req_level MAY >}}使用先前连接中最终的经平滑的RTT值作为恢复出来的连接的初始RTT。如果没有先前的RTT可用，那么初始RTT{{< req_level SHOULD >}}被设置为333毫秒。这能使得握手以1秒的PTO启动，这与TCP初始RTO的推荐值一致；详见《[RFC6298](https://www.rfc-editor.org/info/rfc6298)》的[第2章](https://www.rfc-editor.org/rfc/rfc6298.html#section-2)。

连接可以使用从发送**通道挑战帧**起至接收到**回复通道帧**为止所经过的时间来为新路径设置初始RTT（详见[附录A.2](#A.2_Constants_of_Interest)中的`kInitialRtt`），但是该时间{{< req_level SHOULD_NOT >}}被取作RTT样本。

当初始密钥和握手密钥被弃用后（详见[第6.4章](#6.4_Discarding_Keys_and_Packet_State)），无法确认任何初始数据包和握手数据包，所以可以将它们从在途字节计数中移除。当弃用初始密钥或握手密钥时，{{< req_level MUST >}}重置PTO和丢包检测计时器，因为弃用密钥表明了进度的推进，而丢包检测计时器可能是为已弃用的数据包号空间设置的。
