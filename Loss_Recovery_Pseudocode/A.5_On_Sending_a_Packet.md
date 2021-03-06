---
title: "A.5. 在发送数据包时"
anchor: "A.5_On_Sending_a_Packet"
weight: 10050
rank: "h2"
---

在发送某个数据包后，有关该数据包的信息会被储存。`OnPacketSent`的参数已在上文的[附录A.1.1](#A.1.1_Sent_Packet_Fields)中描述。

`OnPacketSent`的伪代码如下：

{{% block_ref
indx="Pseudocode_10_5_1" %}}

```
OnPacketSent(packet_number, pn_space, ack_eliciting,
             in_flight, sent_bytes):
  sent_packets[pn_space][packet_number].packet_number =
                                           packet_number
  sent_packets[pn_space][packet_number].time_sent = now()
  sent_packets[pn_space][packet_number].ack_eliciting =
                                           ack_eliciting
  sent_packets[pn_space][packet_number].in_flight = in_flight
  sent_packets[pn_space][packet_number].sent_bytes = sent_bytes
  if (in_flight):
    if (ack_eliciting):
      time_of_last_ack_eliciting_packet[pn_space] = now()
    OnPacketSentCC(sent_bytes)
    SetLossDetectionTimer()
```

{{% /block_ref %}}
