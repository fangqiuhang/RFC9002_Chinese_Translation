---
title: "6. 丢包检测"
anchor: "6_Loss_Detection"
weight: 6000
rank: "h1"
---

QUIC senders use acknowledgments to detect lost packets and a PTO to ensure acknowledgments are received; see Section 6.2. This section provides a description of these algorithms.

QUIC发送方使用确认来检测遭遇丢包的数据包，使用PTO来确保确认已被接收到；详见[第6.2章]()。本章描述了这些算法。

If a packet is lost, the QUIC transport needs to recover from that loss, such as by retransmitting the data, sending an updated frame, or discarding the frame. For more information, see Section 13.3 of [QUIC-TRANSPORT].

如果某数据包遭遇丢包，那么QUIC传输需要从该丢包的状态中恢复，例如通过重传数据、发送更新后的帧或放弃传输该帧的的方式。更多信息详见《[QUIC传输]()》的[第13.3章]()。

Loss detection is separate per packet number space, unlike RTT measurement and congestion control, because RTT and congestion control are properties of the path, whereas loss detection also relies upon key availability.

不像RTT测量和拥塞控制那样，每个数据包号空间中的丢包检测是独立的，因为RTT和拥塞控制都是路径的某些属性，而丢包检测还依赖着密钥的可用性。