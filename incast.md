# TCP Incast

## [SIGCOMM '09] Safe and effective fine-grained TCP retransmissions for datacenter communication

- TCP incast collapse:
  - Burst and fast data transmissions overfill Ethernet switch buffers, causing intense packet loss that leads to TCP timeouts.
- These timeouts and the resulting delay can reduce application throughput by 90%
- Fine-grained TCP retransmissions are necessary